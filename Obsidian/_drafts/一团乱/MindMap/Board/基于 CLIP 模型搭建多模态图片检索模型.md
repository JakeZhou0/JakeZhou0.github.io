---
profileName: 阿杰维
postId: "977"
postType: post
categories:
  - 1
---

#回收站/行动盒/数据挖掘

> 主要应用预训练模型 [[CLIP]] 进行图像文本检索功能的实现。由于数据集均为中文环境，我们将采用 [[Chinese-CLIP]] 搭建模型。

安装教程请查看：[OFA-Sys/Chinese-CLIP: Chinese version of CLIP which achieves Chinese cross-modal retrieval and representation generation. (github.com)](https://github.com/OFA-Sys/Chinese-CLIP?tab=readme-ov-file#API%E5%BF%AB%E9%80%9F%E4%B8%8A%E6%89%8B)

本此项目参考：[[多模态图文检索——Chinese-CLIP baseline全流程示例]]

流程图：![[CLIP 模型搭建以及应用流程图|100%]]

## 使用 Chinese-CLIP 的优势（为什么使用 Chinese-CLIP）

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

### 微调

可以得出：

1. **学习率（lr）**：目前设置为 3e-6，对于小批量训练（batch_size=48）较为保守。若发现模型在训练初期 loss 下降缓慢或在验证集上性能提升停滞，可以尝试增大初始学习率，并配合学习率调度策略（如 cosine annealing 或者 step decay）。同时，根据 warmup 步数（warmup=100），可以在练初训期缓慢增加学习率至设定值，避免一开始梯度更新过于剧烈。
2. **数据分布不均匀**：对于图像数据分布不均的问题，首先考虑在预处理阶段是否对数据进行了均衡处理，比如对少样本类别进行过采样或对多样本类别进行下采样。同时，在训练过程中，对比学习（Contrastive Learning）本身有助于缓解类别不平衡带来的影响，因为它主要关注样本间的相对相似性而非绝对分类边界。
3. **序列长度（context_length）**：如果发现模型在处理较长或较复杂的文本时性能不佳，可以尝试适当增加 `context_length`，允许模型捕获更多信息。但要注意增加序列长度会增加计算资源消耗。
4. **权重衰减（wd=0.001）**：作为正则化手段，若出现过拟合现象，可以保持或适度增加 weight decay，反之，若模型欠拟合，可以尝试减小此值。
5. **批次大小（batch_size）**：目前设置为 48，如果您有足够的硬件资源支持更大的批次大小，可以尝试增大以加速收敛。但需要注意，较大的批次大小可能影响模型的泛化能力，特别是对比学习中，较大的 batch_size 有利于提高对比多样性和稳定性。
6. **验证间隔（valid_step_interval 和 valid_epoch_interval）**：如果训练过程中希望频繁检查模型在验证集上的表现，可以缩短验证间隔。这样可以及时了解模型在训练过程中的性能变化，以便于做出相应的调整。
7. **数据增强（use_augment）**：已激活了图像数据增强，可以根据实验结果进一步调整增强策略，确保模型能充分学习到不同变换下的图像特征。
8. **梯度累积（accum_freq=1）**：目前设置为累积一次后更新参数，如果内存资源充足且希望加快训练速度，可以增大此值以模拟更大批次的训练效果，但需注意同步更新次数不宜过大，以免影响训练稳定性。
9. **重计算策略（grad_checkpointing）**：已激活重计算策略，有助于节省显存。如果在训练过程中依然遇到显存不足的问题，可以考虑优化模型结构或者进一步裁剪模型规模。

总之，在实践中需要根据模型在训练集和验证集上的具体表现，以及硬件资源限制，灵活调整以上参数，最终目的是使模型在图文检索任务上达到最好的性能。

论文部分重点说明：处理文件遇到的问题后缀名为.jpg，但内容为 gif，还有其他类型的图片，比如 png，但这些 png 图片我们可以选择不用处理，但 gif 的图片必须处理。

![Pasted image 20240421130108.png](https://ajiew.com/wp-content/uploads/2024/04/Pasted-image-20240421130108-1.png)

![Pasted image 20240421130354.png](https://ajiew.com/wp-content/uploads/2024/04/Pasted-image-20240421130354-1.png)

微调参考书：[[23] 如何对 CLIP 进行 fine-tuning？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/658645438)
