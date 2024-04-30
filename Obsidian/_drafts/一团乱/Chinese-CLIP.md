#归档/资源/数据挖掘

> Chinese-CLIP 是一次极其朴素的开源，没错就是 CLIP 的汉化，旨在推动中文社区多模态发展。
>
> 相比于 CLIP 模型，Chinese-CLIP 更适合我们的应用和微调，因为原始的 CLIP 模型只支持英文，对于我们的中文应用来说不够友好。Chinese-CLIP 很好地弥补了这方面的不足，它使用了**大量的中文 - 文图对进行训练**，与 CLIP 模型架构完全一致。
>
 > > 有关 CLIP 的知识，请参考文章 [[CLIP]]

## 关于 Chinese-CLIP

> **Chinese-CLIP 延续了 CLIP 的模型架构**，使用了不同的训练方式以及全新的中文数据集，即在双流架构和对比学习的支持下，能够有效地整合中文的图像和文本信息到一个共享的嵌入空间，并拥有处理多模态数据的能力。初始阶段以预训练的方式设定了两种编码器：**一种是 CLIP 的视觉编码器，另一种是中文版的 RoBERTa 文本编码器**。
> ![[../附件/Pasted image 20240419131647.png]]

## 如何使用 Chinese-CLIP

### Chinese-CLIP 大致训练步骤

1. 冻结 Image Encoder 的所有参数，只训练 Text Encoder（这一动作是基于一个假设：训练好的 vision backbone 已经有很强的能力来抽取视觉特征了）。直到对下游任务没有明显的提升而结束；
2. 让 Image Encoder 的参数参与训练，这样一来 Image Encoder 的参数就可以学习中文图片数据集了。

## Chinese-CLIP 的应用

> 可以发现和 CLIP 是一样，所以 CLIP 可以实施的应用，在 Chinese-CLIP 同样适用，只需要将依赖库以及相应的 model 转换一下就可以了,省下的应用方向就省略不写了

## Chinese-CLIP 模型微调

> CLIP 的源代码中并没有提供微调训练的程序，可以自行手动码，其实结构很简单，损失函数的形式也给出了，即:

```python
# symmetric loss function
labels = np.arange(n)
loss_i = cross.entropy_loss(logits, labels，axis=0)
loss_t = cross.entropy_loss(losits，iatels，axis=1)
loss = (loss_i + loss_t) / 2
```

> 但是里面的训练细节，例如分布式、warmup 步数、学习率、训练步数等等一些加速训练的手段刚接触的人很难些的出来，你以为那就没有办法了吗！
>
> Chinese-CLIP 源码给出了我们训练源码，我们可以使用 Chinese-CLIP 的微调源码去执行 CLIP 或者 Chinese-CLIP，以应用我们想要微调的数据。

> Chinese-CLIP 微调源码比较复杂，涉及了很多。

**Chinese-CLIP 的训练代码位于**：`Chinese-CLIP/cn_clip/training/main.py`

### 微调所需要的参数

参数设置位于：`Chinese-CLIP/cn_clip/training/params.py`

```python
def parse_args():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "--train-data",type=str,required=True, help="Path to the LMDB directory with training data split")
    parser.add_argument("--val-data",type=str,default=None,help="Path to the LMDB directory with validation data split, default to None which disables validation",)
    parser.add_argument("--num-workers", type=int, default=4, help="The number of workers for training dataloader.")
    parser.add_argument("--valid-num-workers", type=int, default=1, help="The number of workers for validation dataloader (if making validation).")
    parser.add_argument("--logs",type=str,default="./logs/",help="Where to store logs. Use None to avoid storing logs.",)
    parser.add_argument("--name",type=str,default="train_clip",help="Optional identifier for the experiment when storing logs. Otherwise use current time.",)
    parser.add_argument("--log-interval", type=int, default=10, help="How often to log loss info.")
    parser.add_argument("--report-training-batch-acc", default=False,action="store_true", help="Whether to report training batch accuracy.")
    parser.add_argument("--batch-size", type=int, default=64, help="Batch size for training per GPU.")
    parser.add_argument( "--valid-batch-size", type=int, default=64, help="Batch size for validation per GPU.")
    parser.add_argument("--max-steps", type=int, default=None, help="Number of steps to train for (in higher priority to --max_epochs).")
    parser.add_argument("--max-epochs", type=int, default=32, help="Number of full epochs to train for (only works if --max_steps is None).")
    parser.add_argument("--valid-step-interval", type=int, default=None, help="The step interval for validation (default to None which disables validation between steps).")
    parser.add_argument("--valid-epoch-interval", type=int, default=1, help="The epoch interval for validation (default to 1, set None to disable validation between epochs).")
    parser.add_argument("--context-length", type=int, default=52, help="The maximum length of input text (include [CLS] & [SEP] tokens). Default to 52.")
    parser.add_argument("--lr", type=float, default=None, help="Learning rate.")
    parser.add_argument("--beta1", type=float, default=None, help="Adam beta 1.")
    parser.add_argument("--beta2", type=float, default=None, help="Adam beta 2.")
    parser.add_argument("--eps", type=float, default=None, help="Adam epsilon.")
    parser.add_argument("--wd", type=float, default=0.2, help="Weight decay.")
    parser.add_argument("--warmup", type=int, default=500, help="Number of steps to warmup for.")
    parser.add_argument("--use-bn-sync",default=False, action="store_true", help="Whether to use batch norm sync.")
    parser.add_argument("--use-augment",default=False,action="store_true", help="Whether to use image augment.")
    parser.add_argument("--skip-scheduler",action="store_true",default=False, help="Use this flag to skip the learning rate decay.",)
    parser.add_argument("--save-epoch-frequency", type=int, default=1, help="How often to save checkpoints by epochs.")
    parser.add_argument("--save-step-frequency", type=int, default=-1, help="How often to save checkpoints by steps.")
…
…
```

**参数解释：**
- 分布式  
	
- `WORKER_CNT`: 训练的机器个数  
	
- `GPUS_PER_NODE`: 每个机器上的 GPU 个数  
	
- 训练/验证数据  
	
- `train-data`: 训练数据 LMDB 目录，  
	
- `val-data`: 验证数据 LMDB 目录，指定为 None 时，则不进行训练过程中的验证。
- `num-workers`: 训练集数据处理（DataLoader）的进程数，默认为 4。
- `valid-num-workers`: 验证集数据处理（DataLoader）的进程数（如果进行验证），默认为 1。  
	
- 训练超参数  
	
- `vision-model`: 指定视觉 backbone, 从 `["ViT-B-16", "ViT-L-14", "ViT-L-14-336", "ViT-H-14", "RN50"]` 选择。  
	
- `text-model`: 指定文本 backbone, 从 `["RoBERTa-wwm-ext-base-chinese", "RoBERTa-wwm-ext-large-chinese", "RBT3-chinese"]` 选择。  
	
- `context-length`: 文本输入序列长度。  
	
- `warmup`: warmup 步数。  
	
- `batch-size`: 训练时单卡 batch-size。（请保证 `训练样本总数 > batch-size * GPU数`，至少满足 1 个训练 batch）  
	
- `lr`: 学习率。  
	
- `wd`: weight decay。  
	….  
	….  
	**（具体参考 github 中给出的细节）**  

**参数的设置**：

可以参考位于 `run_scripts/muge_finetune_vit-b-16-rbt-base.sh` 中给出的超参数

**然后可以执行 `run_scripts/muge_finetune_vit-b-16-rbt-base.sh` 以进行微调，下面的介绍可以选择不看，如果对源码中的细节感兴趣，想了解分布式，冻结等操作的可以看一下**

### Train 源码解析

`Chinese-CLIP/cn_clip/training/main.py`

1. 解析参数：调用了一个叫做 `parse_args` 的函数，解析并获取命令行传入参数，并将其存储在 `args` 变量中。

`args = parse_args()`

1. 设置分布式训练环境：首先根据环境变量设置本地设备的排名、所使用的 CUDA 设备，并将其存储在 `args` 变量中。然后初始化分布式训练组，使用了 NCCL 作为后端，最后获取当前进程的 rank 和整个训练环境的 world_size，并将其存储在 `args` 变量中。

```text
args.local_device_rank = int(os.environ["LOCAL_RANK"])  
torch.cuda.set_device(args.local_device_rank)
args.device = torch.device("cuda", args.local_device_rank)
dist.init_process_group(backend="nccl")
args.rank = dist.get_rank()
args.world_size = dist.get_world_size()
```

1. 设置输出路径：使用当前时间生成一个时间戳，并根据时间戳设置日志文件的路径和检查点的路径。如果当前进程是主进程，会根据参数创建对应的目录。

```text
time_suffix = strftime("%Y-%m-%d-%H-%M-%S", gmtime())
args.log_path = os.path.join(args.logs, args.name, "out_{}.log".format(time_suffix))

args.checkpoint_path = os.path.join(args.logs, args.name, "checkpoints")
if is_master(args):
    for dirname in [args.checkpoint_path]:
        if dirname:
            os.makedirs(dirname, exist_ok=True)
```

1. 检查精度参数：用于确保 args.precision 的取值在指定范围内，即 'amp'、'fp16' 或 'fp32'

`assert args.precision in ['amp', 'fp16', 'fp32']`

1. 设置日志记录：设置了日志级别，并初始化了日志队列，进而进行了一些日志记录的准备工作。

```text
args.log_level = logging.DEBUG if args.debug else logging.INFO
log_queue = setup_primary_logging(args.log_path, args.log_level, args.rank)
setup_worker_logging(args.rank, log_queue, args.log_level)
```

6.构建 CLIP 模型：这里根据传入的参数，拼接了视觉模型和文本模型的配置文件路径，然后加载并解析了视觉模型和文本模型的配置文件，将其存储在 model_info 中，最后将 args.use_flash_attention 设置到 model_info 中。最后构建了 CLIP 模型实例，并传入了 model_info 中的参数

```text
vision_model_config_file = Path(__file__).parent.parent / f"clip/model_configs/{args.vision_model.replace('/', '-')}.json"
text_model_config_file = Path(__file__).parent.parent / f"clip/model_configs/{args.text_model.replace('/', '-')}.json"

with open(vision_model_config_file, 'r') as fv, open(text_model_config_file, 'r') as ft:
    model_info = json.load(fv)
    if isinstance(model_info['vision_layers'], str):
        model_info['vision_layers'] = eval(model_info['vision_layers'])
    for k, v in json.load(ft).items():
        model_info[k] = v
model_info['use_flash_attention'] = args.use_flash_attention

model = CLIP(**model_info)
```

1. 加载预训练权重：加载预训练的 CLIP 模型权重和 BERT 模型权重，用于 fine-tuning 或推理过

```text
if args.clip_weight_path is not None:
    assert os.path.exists(args.clip_weight_path), "Pretrained CLIP weight not exists!"
if args.bert_weight_path is not None:
    assert os.path.exists(args.bert_weight_path), "Pretrained BERT weight not exists!"
load(model, clip_path=args.clip_weight_path, bert_path=args.bert_weight_path, use_flash_attention=args.use_flash_attention)
```

1. 检查 32 精度：首先检查精度参数是否为 "amp" 或 "fp32"，如果是的话，则调用 convert_models_to_fp32 函数，将模型参数转换为 32 位浮点数。并将模型移动到对应的 GPU 设备上

```text
if args.precision == "amp" or args.precision == "fp32":
    convert_models_to_fp32(model)
model.cuda(args.local_device_rank)
```

1. 检查 16 精度：如果精度参数是 "fp16"，则调用 `convert_weights` 函数，将模型中的权重转换为半精度浮点数。

```text
if args.precision == "fp16":
    convert_weights(model)
```

10.梯度检查点：如果选择了梯度检查点，则首先确保所使用的 PyTorch 版本不小于 1.8.0，然后调用 `set_grad_checkpointing` 函数激活梯度检查点功能，并记录日志信息。

```text
if args.grad_checkpointing:
    assert not torch_version_str_compare_lessequal(torch.__version__, "1.8.0"), \
        "Currently our grad_checkpointing is not compatible with torch version <= 1.8.0."
    model.set_grad_checkpointing()
    logging.info("Grad-checkpointing activated.")
```

1. FlashAttention：如果选择了使用 FlashAttention，则先确保 FlashAttention 库已安装，然后记录日志表示正在使用 FlashAttention。

```text
if args.use_flash_attention:
    assert importlib.util.find_spec("flash_attn"), "flash_attn is not installed."
    logging.info("Using FlashAttention.")
```

1. BatchNorm：如果选择使用同步的 BatchNorm 操作，则调用函数将模型转换为同步 BatchNorm 形式

```text
if args.use_bn_sync:
    model = torch.nn.SyncBatchNorm.convert_sync_batchnorm(model)
```

1. 冻结视觉模型：如果选择冻结视觉编码器（`args.freeze_vision`），则将视觉编码器的参数设置为不可训练。如果视觉模型是 ResNet-50（`args.vision_model` 为 'RN50'），还将 BatchNorm 层的运行均值和方差设置为评估模式，以防止在训练过程中更新这些统计信息。记录日志信息表示视觉编码器在训练期间被冻结。

```text
if args.freeze_vision:
    for k, v in model.visual.named_parameters():
        v.requires_grad = False
    if args.vision_model in ['RN50']:
        for m in model.visual.modules():
            if isinstance(m, torch.nn.BatchNorm2d):
                m.eval()
    logging.info("The visual encoder is freezed during training.")
```

1. 初始化数据：使用 `get_data` 函数初始化数据集

```text
data = get_data(args, epoch_id=0, max_txt_length=args.context_length)
```

15.初始化数据集、优化器、学习率调度器和梯度缩放器，为模型的训练做准备:

```text
if args.train_data is None:
    optimizer = None
    scheduler = None
else:
    optimizer = optim.AdamW(
        [
            {"params": gain_or_bias_params, "weight_decay": 0.},
            {"params": rest_params, "weight_decay": args.wd},
        ],
        lr=args.lr,
        betas=(args.beta1, args.beta2),
        eps=args.eps,
    )
    num_batches = data["train"].dataloader.num_batches
    if args.max_steps is not None:
        args.max_epochs = ceil(args.max_steps * args.accum_freq / num_batches)
    else:
        assert args.max_epochs is not None and args.max_epochs > 0
        args.max_steps = (num_batches // args.accum_freq) * args.max_epochs
    total_steps = args.max_steps
    scheduler = cosine_lr(optimizer, args.lr, args.warmup, total_steps)
```

1. 加载检查点权重：加载检查点文件中保存的模型权重，并根据需要对模型进行相应的操作。如果指定了使用 `flash_attention`，会对模型进行调整。然后会加载模型的状态字典并恢复模型的状态。如果不指定重置数据偏移，会恢复训练的起始 epoch 和步数，并重新加载相应的数据集和数据加载器。如果不指定重置优化器，会恢复优化器的状态

```text
 if args.resume is None:
        latest_path = os.path.join(args.checkpoint_path, f"epoch_latest.pt")
        if os.path.isfile(latest_path):
            args.resume = latest_path
    if args.resume is not None:
        if os.path.isfile(args.resume):
            logging.info(
                f"=> begin to load checkpoint '{args.resume}'"
            )
            checkpoint = torch.load(args.resume, map_location="cpu")
            sd = {k: v for k, v in checkpoint["state_dict"].items() if "bert.pooler" not in k}
            resize_pos_embed(sd, model, prefix="module.")
            if args.use_flash_attention:
                sd = convert_state_dict(sd)
            model.load_state_dict(sd)
            if not args.reset_data_offset:
                start_epoch = checkpoint["epoch"]
                steps = checkpoint["step"]
                data = get_data(args, epoch_id=start_epoch,max_txt_length=args.context_length)
            if not args.reset_optimizer and optimizer is not None:
                optimizer.load_state_dict(checkpoint["optimizer"])
                logging.info("=> optimizer state is restored from the checkpoint")
            logging.info(f"=> loaded checkpoint '{args.resume}' (epoch {checkpoint['epoch']} @ {steps} steps)")
        else:
            logging.info("=> no checkpoint found at '{}'".format(args.resume))
```

1. 进行训练状态：遍历每个 epoch，每个 epoch 内，首先判断当前进程是否为主进程（通过 `is_master(args)` 函数来判断）。如果不是主进程，打印当前 epoch 的信息。如果使用了知识蒸馏（distillation）的方法（`args.distllation=True`），则调用 `train` 函数来进行模型训练，并传入额外的参数 `teacher_model`。否则，只调用 `train` 函数进行模型训练。`train` 函数会返回每个 epoch 中进行的训练步数 `num_steps_this_epoch`。

```text
for epoch in range(start_epoch, args.max_epochs):
     if is_master(args) == 0:
            logging.info(f'Start epoch {epoch + 1}')
     if args.distllation:
            num_steps_this_epoch = train(model, data, epoch, optimizer, scaler, scheduler, args, steps, teacher_model)
     else:
            num_steps_this_epoch = train(model, data, epoch, optimizer, scaler, scheduler, args, steps)
```

- train(model, data, epoch, optimizer, scaler, scheduler, args, steps, teacher_model)：（代码简单，不细致讲解了）将模型设置为训练模式，并根据需要冻结视觉部分的参数。获取训练数据集的 dataloader 和 sampler。定义图像和文本的交叉熵损失函数。设置每个 epoch 的批次数，并迭代训练数据。对每个 batch 进行训练：对图像和文本进行前向传播计算损失。根据训练精度设置是否采用混合精度训练。更新模型参数，并进行相关的记录和日志输出。在特定的训练步骤进行验证集的评估，并保存模型参数。返回该 epoch 训练的步数。

```text
def train(model, data, epoch, optimizer, scaler, scheduler, args, global_trained_steps):
    model.train()
    if args.freeze_vision:
        freeze_vision_bn(args, model)
    dataloader, sampler = data['train'].dataloader,  data['train'].sampler
    loss_img = nn.CrossEntropyLoss()
    loss_txt = nn.CrossEntropyLoss()
    loss_img = loss_img.cuda(args.local_device_rank)
    loss_txt = loss_txt.cuda(args.local_device_rank)
    if sampler is not None:
        sampler.set_epoch(epoch)
    num_batches_per_epoch = dataloader.num_batches
    data_iter = iter(dataloader)
    end = time.time()
    epoch_trained_steps = 0
    for i in range(global_trained_steps - num_batches_per_epoch * epoch, num_batches_per_epoch):
        batch = next(data_iter)
        step = num_batches_per_epoch * epoch + i
        if step >= args.max_steps:
            logging.info("Stopping training due to step {} has reached max_steps {}".format(step, args.max_steps))
            return epoch_trained_steps
        scheduler(step)
        optimizer.zero_grad()
        images, texts, eos_indices = batch
        images = images.cuda(args.local_device_rank, non_blocking=True)
        texts = texts.cuda(args.local_device_rank, non_blocking=True)
        eos_indices = eos_indices.cuda(args.local_device_rank, non_blocking=True)
        data_time = time.time() - end
        m = model.module
        # with automatic mixed precision.
        if args.precision == "amp":
            with autocast():
                total_loss, acc = get_loss(model, images, texts, loss_img, loss_txt, args)
                scaler.scale(total_loss).backward()
                scaler.step(optimizer)
            scaler.update()
        else:
            total_loss, acc = get_loss(model, images, texts, loss_img, loss_txt, args)
            total_loss.backward()
            optimizer.step()
            ….
```

1. 验证数据：如果指定了验证数据集（`args.val_data` 不为 None）和验证间隔（`args.valid_epoch_interval` 不为 None），并且当前 epoch 是验证的时间点（`(epoch + 1) % args.valid_epoch_interval == 0`），则调用 `evaluate` 函数对模型进行验证。如果没有使用闪躲注意力（flash attention），直接调用 `evaluate` 函数；否则，在使用了半精度训练（fp16）的情况下，使用 `torch.cuda.amp.autocast()` 上下文管理器来运行 `evaluate` 函数，以确保模型在 GPU 上运行。如果还存在下一个 epoch（`epoch + 1 < args.max_epochs`），则重新加载下一个 epoch 的数据集和数据加载器。

```text
steps += num_steps_this_epoch
if args.val_data is not None and args.valid_epoch_interval is not None and (
        (epoch + 1) % args.valid_epoch_interval) == 0:
    assert "val" in data, "Error: Valid dataset has not been built."
    if not args.use_flash_attention:
        evaluate(model, data, epoch, args, steps)
    else:
        with torch.cuda.amp.autocast():
            evaluate(model, data, epoch, args, steps)
if epoch + 1 < args.max_epochs:
    data = get_data(args, epoch_id=epoch + 1, max_txt_length=args.context_length)
```

## 图文相似度的计算

示例代码：

```python
import torch 
from PIL import Image

import cn_clip.clip as clip
from cn_clip.clip import load_from_name, available_models
print("Available models:", available_models())  
# Available models: ['ViT-B-16', 'ViT-L-14', 'ViT-L-14-336', 'ViT-H-14', 'RN50']

device = "cuda" if torch.cuda.is_available() else "cpu"
model, preprocess = load_from_name("ViT-B-16", device=device, download_root='./')
model.eval()
image = preprocess(Image.open("examples/pokemon.jpeg")).unsqueeze(0).to(device)
text = clip.tokenize(["杰尼龟", "妙蛙种子", "小火龙", "皮卡丘"]).to(device)

with torch.no_grad():
    image_features = model.encode_image(image)
    text_features = model.encode_text(text)
    # 对特征进行归一化，请使用归一化后的图文特征用于下游任务
    image_features /= image_features.norm(dim=-1, keepdim=True) 
    text_features /= text_features.norm(dim=-1, keepdim=True)    

    logits_per_image, logits_per_text = model.get_similarity(image, text)
    probs = logits_per_image.softmax(dim=-1).cpu().numpy()

print("Label probs:", probs)  # [[1.268734e-03 5.436878e-02 6.795761e-04 9.436829e-01]]
```

## 图文检索（Top-k）

示例代码

```python
import torch
import clip
from PIL import Image

device = "cuda" if torch.cuda.is_available() else "cpu"
model, preprocess = clip.load("ViT-B/32", device=device)

image = preprocess(Image.open("CLIP.png")).unsqueeze(0).to(device)
text = clip.tokenize(["a diagram", "a dog", "a cat","a yellow dog","a running dog"]).to(device)

with torch.no_grad():
    image_features = model.encode_image(image)
    text_features = model.encode_text(text)

image_features /= image_features.norm(dim=-1, keepdim=True)
text_features /= text_features.norm(dim=-1, keepdim=True)
similarity = (100.0 * image_features @ text_features.T).softmax(dim=-1)
values, indices = similarity[0].topk(3)
print(values,indices)
```

> 还有其他跟多的应用这里不一一列出。

## 参考文献

- [多模态表征—CLIP及中文版Chinese-CLIP：理论讲解、代码微调与论文阅读 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/690361706)
- [OFA-Sys/Chinese-CLIP: Chinese version of CLIP which achieves Chinese cross-modal retrieval and representation generation. (github.com)](https://github.com/OFA-Sys/Chinese-CLIP)
- [[2211.01335v2] Chinese CLIP: Contrastive Vision-Language Pretraining in Chinese (arxiv.org)](https://arxiv.org/abs/2211.01335v2)
