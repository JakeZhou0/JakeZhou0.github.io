#回收站/知识盒/数据挖掘/图文检索/CLIP

## 准备工作

### 1. Clone 代码库并准备数据目录

```python
# clone Chinese-CLIP代码库到用户目录(如果因网络问题卡在git clone这步，请interrupt该步并重试几次)：
!git clone https://github.com/OFA-Sys/Chinese-CLIP.git

# 创建一个datapath文件夹，用于存放数据集和Chinese-CLIP参数
!mkdir -p datapath
!mkdir -p datapath/pretrained_weights # 存放预训练参数
!mkdir -p datapath/datasets # 存放数据集
!mkdir -p datapath/experiments # 存放finetune参数和日志

!tree .
```

### 2. 安装 Chinese-CLIP 相关依赖

```python
# 安装Chinese-CLIP依赖包
!pip install -r Chinese-CLIP/requirements.txt
# 查看当前kernel下已安装的包  list packages
!pip list --format=columns
```

### 3. 下载 Chinese-CLIP 预训练参数

```python
# 下载base规模Chinese-CLIP预训练参数：

!wget https://clip-cn-beijing.oss-cn-beijing.aliyuncs.com/checkpoints/clip_cn_vit-b-16.pt

!mv clip_cn_vit-b-16.pt datapath/pretrained_weights/
```

### 4. 预处理数据

[[目录结构转化成适合Chinese-CLIP项目的目录结构和数据格式]]

```python
# 详细的预处理数据流程，请参见github readme: https://github.com/OFA-Sys/Chinese-CLIP#数据集格式预处理

# 我们这里方便起见，直接下载已经预处理好（处理成LMDB格式）的电商检索数据集

!wget https://clip-cn-beijing.oss-cn-beijing.aliyuncs.com/datasets/MUGE.zip

!mv MUGE.zip datapath/datasets/

%cd datapath/datasets/

!unzip MUGE.zip

%cd ../..

!tree datapath/
```

```python
# 查看数据样例

!head -n 1 datapath/datasets/MUGE/valid_texts.jsonl # 验证集第一条样本

  

import lmdb

import base64

from io import BytesIO

from PIL import Image

  

image_ids = [286314, 141999, 183846]

  

lmdb_imgs = "datapath/datasets/MUGE/lmdb/valid/imgs"

env_imgs = lmdb.open(lmdb_imgs, readonly=True, create=False, lock=False, readahead=False, meminit=False)

txn_imgs = env_imgs.begin(buffers=True)

for image_id in image_ids:

    image_b64 = txn_imgs.get("{}".format(image_id).encode('utf-8')).tobytes()

    img = Image.open(BytesIO(base64.urlsafe_b64decode(image_b64)))

    img.show()
```

## 运行 Finetune 训练

```python
# 进入代码工作区目录

%cd Chinese-CLIP/ # 666
```

下面我们开始运行 finetune，说明如下：

+ 下面的代码改编自代码库中的 shell 运行脚本: Chinese-CLIP/run_scripts/muge_finetune_vit-b-16_rbt-base.sh
+ **详细的 finetune 各配置项，请参见: <https://github.com/OFA-Sys/Chinese-CLIP>模型 finetune**
+ 执行训练的 python 代码，请参见: Chinese-CLIP/cn_clip/training/main.py，
+ 模型实现的 python 代码，请参见: Chinese-CLIP/cn_clip/clip/model.py 以及比赛官方学习视频对于模型实现的介绍
+ 按照如下的超参进行 finetune，要求机器需要至少达到 8G 显存，finetune 时间大约需要 40min 左右（V100 上测试）
+ **请注意 finetune 中间给出的验证集准确率，是验证集 batch 内部，图文对之间的 Recall@1 正确率，与比赛指标要求的从整个验证集/测试集图片池召回的 Recall@1 并不是同一个指标。这里仅用于观察训练趋势，如果要评测模型效果，请完整运行下文的特征提取、KNN 召回和计算 Recall 流程**
+ 对比学习的训练收敛和稳定性和总 batch size 相关。如您使用较小的 batch size（比如我们这里的 48 per-GPU * 1 GPU），建议使用较小的学习率（如我们这里的 3e-6）。我们推荐使用更多的 GPU 和更大的 batch size 以取得更好的效果。
+ 训练完成后如果输出打印 EOFError，无视即可

```python
# 准备finetune相关配置，详见https://github.com/OFA-Sys/Chinese-CLIP#模型finetune

# 指定机器数 & 卡数

GPUS_PER_NODE=1 # 卡数

WORKER_CNT=1 # 机器数

MASTER_ADDR="localhost"

MASTER_PORT=8514 # 同台机器同时起多个任务，请分别分配不同的端口号

RANK=0

  

# 刚刚创建过的目录，存放了预训练参数和预处理好的数据集

DATAPATH="../datapath/"

  

# 指定LMDB格式的训练集和验证集路径（存放了LMDB格式的图片和图文对数据）

train_data=f"{DATAPATH}/datasets/MUGE/lmdb/train"

val_data=f"{DATAPATH}/datasets/MUGE/lmdb/valid"

num_workers=4 # 训练集pytorch dataloader的进程数，设置为>0，以减小训练时读取数据的时间开销

valid_num_workers=4 # 验证集pytorch dataloader的进程数，设置为>0，以减小验证时读取数据的时间开销

  

# 指定刚刚下载好的Chinese-CLIP预训练权重的路径

resume=f"{DATAPATH}/pretrained_weights/clip_cn_vit-b-16.pt"

reset_data_offset="--reset-data-offset" # 从头读取训练数据

reset_optimizer="--reset-optimizer" # 重新初始化AdamW优化器

  

# 指定输出相关配置

output_base_dir=f"{DATAPATH}/experiments/"

name="muge_finetune_vit-b-16_roberta-base_bs48_1gpu" # finetune超参、日志、ckpt将保存在../datapath/experiments/muge_finetune_vit-b-16_roberta-base_bs48_1gpu/

save_step_frequency=999999 # disable it

save_epoch_frequency=1 # 每轮保存一个finetune ckpt

log_interval=10 # 日志打印间隔步数

report_training_batch_acc="--report-training-batch-acc" # 训练中，报告训练batch的in-batch准确率

  

# 指定训练超参数

context_length=52 # 序列长度，这里指定为Chinese-CLIP默认的52

warmup=100 # warmup步数

batch_size=48 # 训练单卡batch size

valid_batch_size=48 # 验证单卡batch size

lr=3e-6 # 学习率，因为这里我们使用的对比学习batch size很小，所以对应的学习率也调低一些

wd=0.001 # weight decay

max_epochs=1 # 训练轮数，也可通过--max-steps指定训练步数

valid_step_interval=1000 # 验证步数间隔

valid_epoch_interval=1 # 验证轮数间隔

vision_model="ViT-B-16" # 指定视觉侧结构为ViT-B/16

text_model="RoBERTa-wwm-ext-base-chinese" # 指定文本侧结构为RoBERTa-base

use_augment="--use-augment" # 对图像使用数据增强

grad_checkpointing="--grad-checkpointing" # 激活重计算策略，用更多训练时间换取更小的显存开销

  

run_command = "export PYTHONPATH=${PYTHONPATH}:`pwd`/cn_clip;" + \

f"""

python3 -m torch.distributed.launch --nproc_per_node={GPUS_PER_NODE} --nnodes={WORKER_CNT} --node_rank={RANK} \

      --master_addr={MASTER_ADDR} --master_port={MASTER_PORT} cn_clip/training/main.py \

      --train-data={train_data} \

      --val-data={val_data} \

      --num-workers={num_workers} \

      --valid-num-workers={valid_num_workers} \

      --resume={resume} \

      {reset_data_offset} \

      {reset_optimizer} \

      --logs={output_base_dir} \

      --name={name} \

      --save-step-frequency={save_step_frequency} \

      --save-epoch-frequency={save_epoch_frequency} \

      --log-interval={log_interval} \

      {report_training_batch_acc} \

      --context-length={context_length} \

      --warmup={warmup} \

      --batch-size={batch_size} \

      --valid-batch-size={valid_batch_size} \

      --valid-step-interval={valid_step_interval} \

      --valid-epoch-interval={valid_epoch_interval} \

      --lr={lr} \

      --wd={wd} \

      --max-epochs={max_epochs} \

      --vision-model={vision_model} \

      {use_augment} \

      {grad_checkpointing} \

      --text-model={text_model}

""".lstrip()

print(run_command)
```

```python
# 执行finetune流程

!{run_command}
```

## 验证集效果验证

为了验证模型的效果，我们提供特征提取、以及图文检索任务评估的流程。更加详尽的描述，也可参考 Github readme 的相关部分说明：<https://github.com/OFA-Sys/Chinese-CLIP/blob/master/README.md>

### 1. 计算图文特征

```python
# 为验证集图片池和query文本计算特征

dataset_name="MUGE"

split="valid" # 指定计算valid或test集特征

# 指定我们刚刚finetune的ckpt路径，也可以指定预训练ckpt路径测试zero-shot效果

resume=f"{DATAPATH}/experiments/muge_finetune_vit-b-16_roberta-base_bs48_1gpu/checkpoints/epoch_latest.pt"

  

run_command = "export PYTHONPATH=${PYTHONPATH}:`pwd`/cn_clip;" + \

f"""

python -u cn_clip/eval/extract_features.py \

    --extract-image-feats \

    --extract-text-feats \

    --image-data="{DATAPATH}/datasets/{dataset_name}/lmdb/{split}/imgs" \

    --text-data="{DATAPATH}/datasets/{dataset_name}/{split}_texts.jsonl" \

    --img-batch-size=32 \

    --text-batch-size=32 \

    --context-length=52 \

    --resume={resume} \

    --vision-model=ViT-B-16 \

    --text-model=RoBERTa-wwm-ext-base-chinese

"""

print(run_command.lstrip())

!{run_command}
```

产出图文特征将保存于 `../datapath/datasets/MUGE` 目录下，图片特征保存于 `valid_imgs.img_feat.jsonl` 文件，每行以 json 存储一张图片的特征，格式如下：

```
{"image_id": 1000002, "feature": [0.0198, …, -0.017, 0.0248]}
```

文本特征则保存于 `valid_texts.txt_feat.jsonl`，格式如下：

```
{"text_id": 248816, "feature": [0.1314, …, 0.0018, -0.0002]}
```

### 2. KNN 检索

对于小规模的学术检索数据集，我们提供一个简单的 KNN 检索实现，便于计算文到图检索，在验证集 3w 图片池的 top-k 召回结果。

```python
# 进行KNN检索，为验证集每个query，匹配特征余弦相似度最高的top-10商品图片

  

split="valid" # 指定计算valid或test集特征

  

run_command = "export PYTHONPATH=${PYTHONPATH}:`pwd`/cn_clip;" + \

f"""

python -u cn_clip/eval/make_topk_predictions.py \

    --image-feats="{DATAPATH}/datasets/{dataset_name}/{split}_imgs.img_feat.jsonl" \

    --text-feats="{DATAPATH}/datasets/{dataset_name}/{split}_texts.txt_feat.jsonl" \

    --top-k=10 \

    --eval-batch-size=32768 \

    --output="{DATAPATH}/datasets/{dataset_name}/{split}_predictions.jsonl"

"""

print(run_command.lstrip())

!{run_command}
```

产出的结果保存在指定的 jsonl 文件中，每行表示一个文本召回的 top-k 图片 id（按模型相关性预测分数由大到小排好了序），格式如下，这个格式和我们比赛要求的提交格式是一样的：

```
!head -n 5 ../datapath/datasets/MUGE/valid_predictions.jsonl
```

我们具体观察其中一组 case 的预测结果：

```python
# 查看数据样例

!sed -n "5,5p" ../datapath/datasets/MUGE/valid_texts.jsonl # 验证集第三条样本，对应上面第5行

  

import lmdb

import base64

from io import BytesIO

from PIL import Image

  

image_ids = [225106, 139500, 349934, 941660, 515959] # 模型预测的top-5相关图片

  

lmdb_imgs = "../datapath/datasets/MUGE/lmdb/valid/imgs"

env_imgs = lmdb.open(lmdb_imgs, readonly=True, create=False, lock=False, readahead=False, meminit=False)

txn_imgs = env_imgs.begin(buffers=True)

for image_id in image_ids:

    image_b64 = txn_imgs.get("{}".format(image_id).encode('utf-8')).tobytes()

    img = Image.open(BytesIO(base64.urlsafe_b64decode(image_b64)))

    img.show()
```

### 3. Recall 计算

我们提供了评测脚本计算检索任务的 Recall@1/5/10，同时给出 mean recall（Recall@1/5/10 的平均数）。运行如下命令即可获取分数:

```python
# 根据top-10预测结果，计算验证集的Recall@1/5/10，同时给出mean recall（Recall@1/5/10的平均数）

  

split="valid" # 指定计算valid或test集特征

  

run_command = "export PYTHONPATH=${PYTHONPATH}:`pwd`/cn_clip;" + \

f"""

python cn_clip/eval/evaluation.py \

    {DATAPATH}/datasets/{dataset_name}/{split}_texts.jsonl \

    {DATAPATH}/datasets/{dataset_name}/{split}_predictions.jsonl \

    output.json;

cat output.json

"""

print(run_command.lstrip())

!{run_command}
```

可以看到验证集上，我们取得了~75 的 Mean Recall 值，同时也给出了详细的 Recall@1/5/10. 这个分数，已经比直接使用同规模预训练 ckpt 进行预测（zero-shot）的 71.1 更高，说明我们的 finetune 让模型更加适配到电商检索任务的领域数据上。通过调节不同的超参，上面 finetune 的分数还有很大的提升空间。在我们的实验中，Chinese-CLIP 各规模 zero-shot 以及 finetune，在验证集上可以得到的分数大体如下（更多 Chinese-CLIP 在其他任务的实验结果，请详见 Github 代码库 <https://github.com/OFA-Sys/Chinese-CLIP/blob/master/Results.md> ）：

**MUGE Text-to-Image Retrieval (Official Validation Set)**:

<table border="1" width="100%">
	<tr align="center">
		<th>Setup</th><th colspan="4">Zero-shot</th><th colspan="4">Finetune</th>
	</tr>
	<tr align="center">
		<td>Metric</td><td>R@1</td><td>R@5</td><td>R@10</td><td>MR</td><td>R@1</td><td>R@5</td><td>R@10</td><td>MR</td>
	</tr>
	<tr align="center">
		<td>CN-CLIP<sub>RN50</sub></td><td>42.6</td><td>68.6</td><td>77.9</td><td>63.0</td><td>48.6</td><td>75.1</td><td>84.0</td><td>69.2</td>
	</tr>  
	<tr align="center">
		<td>CN-CLIP<sub>ViT-B/16</sub></td><td>52.1</td><td>76.7</td><td>84.4</td><td>71.1</td><td>58.4</td><td>83.6</td><td>90.0</td><td>77.4</td>
	</tr>
	<tr align="center">
		<td>CN-CLIP<sub>ViT-L/14</sub></td><td>56.3</td><td>79.8</td><td>86.2</td><td>74.1</td><td>63.3</td><td>85.6</td><td>91.3</td><td>80.1</td>
	</tr>  
	<tr align="center">
		<td>CN-CLIP<sub>ViT-L/14@336px</sub></td><td>59.0</td><td>81.4</td><td>87.8</td><td>76.1</td><td>65.3</td><td>86.7</td><td>92.1</td><td>81.3</td>
	</tr>
	<tr align="center">
		<td>CN-CLIP<sub>ViT-H/14</sub></td><td><b>63.0</b></td><td><b>84.1</b></td><td><b>89.2</b></td><td><b>78.8</b></td><td><b>68.9</b></td><td><b>88.7</b></td><td><b>93.1</b></td><td><b>83.6</b></td>
	</tr>
</table>
<br>

## 准备测试集结果

下面我们在测试集上，再运行一次和验证集同样的特征计算和 KNN 召回流程，只是数据换成测试集，从而准备一份测试集预测结果，用于提交官方。

```python
# 为测试集图片池和query文本计算特征

dataset_name="MUGE"

split="test" # 指定计算valid或test集特征

resume=f"{DATAPATH}/experiments/muge_finetune_vit-b-16_roberta-base_bs48_1gpu/checkpoints/epoch_latest.pt"

  

run_command = "export PYTHONPATH=${PYTHONPATH}:`pwd`/cn_clip;" + \

f"""

python -u cn_clip/eval/extract_features.py \

    --extract-image-feats \

    --extract-text-feats \

    --image-data="{DATAPATH}/datasets/{dataset_name}/lmdb/{split}/imgs" \

    --text-data="{DATAPATH}/datasets/{dataset_name}/{split}_texts.jsonl" \

    --img-batch-size=32 \

    --text-batch-size=32 \

    --context-length=52 \

    --resume={resume} \

    --vision-model=ViT-B-16 \

    --text-model=RoBERTa-wwm-ext-base-chinese

"""

print(run_command.lstrip())

!{run_command}
```

```python
# 进行KNN检索，为测试集每个query，匹配特征余弦相似度最高的top-10商品图片

  

split="test" # 指定计算valid或test集特征

  

run_command = "export PYTHONPATH=${PYTHONPATH}:`pwd`/cn_clip;" + \

f"""

python -u cn_clip/eval/make_topk_predictions.py \

    --image-feats="{DATAPATH}/datasets/{dataset_name}/{split}_imgs.img_feat.jsonl" \

    --text-feats="{DATAPATH}/datasets/{dataset_name}/{split}_texts.txt_feat.jsonl" \

    --top-k=10 \

    --eval-batch-size=32768 \

    --output="{DATAPATH}/datasets/{dataset_name}/{split}_predictions.jsonl"

"""

print(run_command.lstrip())

!{run_command}
```

```python
!head -n 5 ../datapath/datasets/MUGE/test_predictions.jsonl
```

该结果下载并提交到天池后，预期将取得 56.5/80.6/87.5 左右的 Recall@1/5/10，即 74.9 左右的 Mean Recall，可能由于 finetune 的随机性有一些小幅度的浮动。
