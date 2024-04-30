s1. **数据集文件组织**：

   **[[训练集和验证集的划分]]**：用户需要将图文数据集划分为训练集（train）、验证集（valid）和测试集（test），并在 `${DATAPATH}/datasets/${dataset_name}` 目录下创建相应的子目录结构。假设 `${dataset_name}` 是 "MUGE"，那么最终的目录树将会如下：

   ```
   ${DATAPATH}
   └── datasets/
       └── MUGE/
           ├── train_imgs.tsv
           ├── train_texts.jsonl
           ├── valid_imgs.tsv
           ├── valid_texts.jsonl
           ├── test_imgs.tsv
           └── test_texts.jsonl
   ```

   在这个结构中：

   - `train_imgs.tsv`：包含训练集中的每张图片 ID 及其 Base64 编码的图片内容。
   - `train_texts.jsonl`：每行是一个 JSON 对象，记录着文本 ID、文本内容以及该文本关联的图片 ID 列表。
   - `valid` 和 `test` 分支类似，对应验证集和测试集的数据。

1. **图片转 Base64 编码**：
   使用 Python 代码片段将原始图片文件转换为 Base64 编码字符串，这样图片就可以作为文本数据嵌入到 `.tsv` 文件中。例如，对一张名为 `image.jpg` 的图片执行上述代码后，会在 `train_imgs.tsv` 文件中新增一行，形如：

   ```
   1000001	/9j/4AAQSkZJRgABAQEAAAAAAAD/2wBD…
   ```

2. **文本信息与图文对关系**：
   在 `train_texts.jsonl` 或 `valid_texts.jsonl` 等文件中，每行都是一个 JSON 对象，如：

   ```json
   {"text_id": 1, "text": "这是一个包包的描述", "image_ids": [20001, 20002]}
   ```

   这表示文本 ID 为 1 的文本描述与图片 ID 为 20001 和 20002 的图片有关联。

3. **测试集特殊情况**：
   对于只包含文本信息的测试集，若无法得知图文对应关系，则将 `image_ids` 字段设置为空数组：

   ```json
   {"text_id": 5000, "text": "这是测试集的纯文本描述", "image_ids": []}
   ```

4. **LMDB 数据库转换**：
   为了进一步提高训练时数据加载的效率，需要将上述 `.tsv` 和 `.jsonl` 文件转换为内存索引的 LMDB 数据库文件。通过运行 `cn_clip/preprocess/build_lmdb_dataset.py` 脚本完成此操作，例如：

   ```shell
   python cn_clip/preprocess/build_lmdb_dataset.py --data_dir ${DATAPATH}/datasets/MUGE --splits train,valid,test
   ```

   这将生成一个新的目录结构，其中包含了 LMDB 数据库文件，如：

   ```
   ${DATAPATH}
   └── datasets/
       └── MUGE/
           └── lmdb/
               ├── train
               │   ├── imgs
               │   └── pairs
               ├── valid
               └── test
   ```

   这些 `lmdb` 子目录内部的数据库文件便于程序随机读取和高效访问图文数据。

总结来说，整个预处理流程就是将原始图文数据整理成特定格式的文本文件，然后转换为内存数据库，使得 Chinese-CLIP 模型能够高效且准确地读取和利用这些数据进行训练、验证和测试。
