#回收站/知识盒/数据挖掘

## 背景

> 2021 年见证了 vision transformer 的大爆发，随着谷歌提出 ViT 之后，一大批的 vision transformer 的工作席卷计算机视觉任务。除了 vision transformer，另外一个对计算机视觉影响比较大的工作就是 Open AI 在 2021 年 1 月份发布的 [DALL-E](https://link.zhihu.com/?target=https%3A//openai.com/blog/dall-e/) 和 [CLIP](https://link.zhihu.com/?target=https%3A//openai.com/blog/clip/)，这两个都属于结合图像和文本的多模态模型，其中**DALL-E 是基于文本来生成模型的模型**，而**CLIP 是用文本作为监督信号来训练可迁移的视觉模型**，这两个工作也像 ViT 一样带动了一波新的研究高潮。这篇文章将首先介绍 CLIP 的原理以及如何用 CLIP 实现 zero-shot 分类，然后我们将讨论 CLIP 背后的动机，最后文章会介绍 CLIP 的变种和其它的一些应用场景。

这是 CLIP 相关的诞生背景，2021 年 google 推出 ViT（vision transformer），除了 ViT，同年另一个比较大的工作就是 Open Ai 在 2021 年 1 月份发布的 DALL-E 和 CLI，这两个都是属于结合图像文本的多模态模型。

## [[CLIP]] 是什么？

> CLIP（Contrastive Language-Image Pre-training）是由 OpenAI 提出的一种多模态深度学习模型，它通过联合训练图像和文本表示，以解决不同模态间（视觉与语言）的信息对应问题（多模态融合问题）。CLIP 的核心思想是利用大量的图像 - 文本对数据集进行预训练，这些数据集通常来源于互联网上的图像及对应的描述性文本。

> 相比传统复杂的交互式的多模态预训练，**CLIP 的模型极为简单**，即我们常说的双塔模型，分别包括**图像塔和文本塔**。图像塔负责提取图像表征，一般为**Vision Transformer**，即常说的 ViT，文本塔则负责提取文本特征，使用经典 Transformer 架构。

在架构上，CLIP 包含两个关键组件：

1. **文本编码器（Text Encoder）**：采用 Transformer 结构，用于将输入的自然语言文本转化为高维向量表示。
2. **图像编码器（Image Encoder）**：可以使用 ResNet 或 Vision Transformer 等视觉模型，将输入的图像转化为相应的高维向量表示。

![[../附件/Pasted image 20240419084657.png]]

预训练过程中，CLIP 通过**对比学习（contrastive learning）方法**，让模型学习到图像和其相关描述文本之间的相似性，并最大化它们之间的关联度，同时最小化与不相关文本对之间的关联度。经过这样的训练后，CLIP 模型能够捕捉到图像与文本之间的语义关系，并展现出强大的**迁移学习能力**（能够在不同视觉任务之间有效地复用学到的知识和特征表示，无需针对每个新任务进行大量的重新训练。），能够在未经特定任务微调的情况下，执行零样本（zero-shot）分类任务，即对于未曾见过类别的新图像，仅凭文本描述就能判断出其所属类别。

CLIP 的创新之处在于打破了传统依赖大量标注数据进行图像分类的方式，大大提高了模型的数据效率和泛化能力，在多个视觉任务上表现出色。

## CLIP 可以做什么？

### **zero-shot 分类**

> 训练后的 CLIP 其实是两个模型，除了视觉模型外还有一个文本模型，那么如何对预训练好的视觉模型进行迁移呢？

#### 如何使用 CLIP 进行迁移任务？

> **CV 中常用的先预训练然后微调不同，CLIP 可以直接实现 zero-shot 的图像分类，即不需要任何训练数据，就能在某个具体下游任务上实现分类，**这也是 CLIP 亮点和强大之处。

使用 CLIP 实现 zero-shot，很简单，仅仅只需三个步骤（具体参考案例：[CLIP/notebooks/Interacting_with_CLIP.ipynb at main · openai/CLIP (github.com)](https://github.com/openai/CLIP/blob/main/notebooks/Interacting_with_CLIP.ipynb)）：

![[../附件/Pasted image 20240419090710.png]]

1. 处理文本，并编码类别提示。

```python
# 定义并编码类别提示
class_texts = ["text prompt for class 1", "text prompt for class 2", …]
class_embeddings = model.encode_text(clip.tokenize(class_texts))
```

1. 处理图像，并转化图像特征。

```python
# 编码图像特征
image_features = model.encode_image(input_image)

# 编码图像特征
image_features = model.encode_image(input_image)
```

1. 计算相似度并预测类别

```python
# 计算相似度
similarities = (image_features @ class_embeddings.T) / temperature

# 预测类别
predicted_class_index = similarities.argmax(dim=-1)
predicted_class_text = class_texts[predicted_class_index]
```

> 可以看到，我们是利用 CLIP 的多模态特性为具体的任务**构建了动态的分类器**，**其中 Text Encoder 提取的文本特征可以看成分类器的 weights，而 Image Encoder 提取的图像特征是分类器的输入**。

### 图像检索

> 基于文本来搜索图像是 CLIP 最能直接实现的一个应用，其实 CLIP 也是作为 DALL-E 的排序模型，即从生成的图像中选择和文本相关性较高的。

### 视频理解

> CLIP 是基于文本 - 图像对来做的，但是它可以扩展到文本 - 视频，比如 [VideoCLIP](https://link.zhihu.com/?target=https%3A//arxiv.org/abs/2109.14084) 就是将 CLIP 应用在视频领域来实现一些 zero-shot 视频理解任务。

### 图像编辑

> CLIP 可以用在指导图像编辑任务上，[HairCLIP](https://link.zhihu.com/?target=https%3A//arxiv.org/abs/2112.05142) 这篇工作用 CLIP 来定制化修改发型：
>
> ![[../附件/Pasted image 20240419093601.png]]

### 图像生成

> CLIP 还可以应用在图像生成上，比如 [StyleCLIP](https://link.zhihu.com/?target=https%3A//arxiv.org/abs/2103.17249) 这篇工作用 CLIP 实现了文本引导的 StyleGAN：
>
 > ![](https://pic4.zhimg.com/v2-5521eeeea9a05902901be084721d343f_r.jpg)
>
> [CLIP-GEN](https://link.zhihu.com/?target=https%3A//arxiv.org/abs/2203.00386) 这篇工作基于 CLIP 来训练文本生成图像模型，训练无需直接采用任何文本数据：
>
> ![](https://pic2.zhimg.com/v2-5a3b349b1f4c87337bbc6b00d19d0e91_r.jpg)

### 自监督学习

> 最近华为的工作 [MVP](https://link.zhihu.com/?target=https%3A//arxiv.org/abs/2203.05175) 更是采用 CLIP 来进行视觉自监督训练：
>
> ![](https://pic2.zhimg.com/v2-3566c78d49a552e75b08b9dca5670a99_r.jpg)

### VL 任务

> CLIP 本身就是多模态模型，所以它也可以用在用图像 - 文本多模态任务，如图像描述（image caption）和视觉问答（Visual Question Answering），这篇论文 [How Much Can CLIP Benefit Vision-and-Language Tasks?](https://link.zhihu.com/?target=https%3A//arxiv.org/abs/2107.06383) 系统评估了 CLIP 在 VL 任务上带来的收益。
>
> ![](https://pic4.zhimg.com/v2-a547b94a9e73fc462fc186b36dbf721b_r.jpg)

## 参考文献

- [神器 CLIP：连接文本和图像，打造可迁移的视觉模型 - 知乎 (zhihu.com)](<https://zhuanlan.zhihu.com/p/493489688>
- [Welcome to Spinning Up in Deep RL! — Spinning Up documentation (openai.com)](https://spinningup.openai.com/en/latest/)
- [【ICLR2021】ViT : Vision Transformer解读（论文+源码） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/418184940)
- [CLIP/notebooks/Interacting_with_CLIP.ipynb at main · openai/CLIP (github.com)](https://github.com/openai/CLIP/blob/main/notebooks/Interacting_with_CLIP.ipynb)
- [多模态表征—CLIP及中文版Chinese-CLIP：理论讲解、代码微调与论文阅读 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/690361706)
