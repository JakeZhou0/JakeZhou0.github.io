600 个插件，提取 8 种进阶用法

如今的笔记软件用户中，很多人会陷入「用笔记软件来记录如何使用笔记软件」的误区。即使避免了这个陷阱，也很可能花过不少功夫整理关于「卡片笔记写作法」（来自同名图书，英文原版题为 _How to take smart notes_）的笔记。还有很多人自觉精通了「心流」，但却只在研究笔记方法论时能沉浸其中，对于真正需要记录的内容则还是只消半小时就能忘掉。

这种「假装高产实则摸鱼」的问题，在很多人初学 Obsidian 时尤为明显——由于这款软件的丰富插件生态，我们一边要学习它不算简单的逻辑，一边还不得不消耗额外的意志力，去对抗那种按耐不住想要折腾插件的冲动；更糟的是每个插件用起来都不简单。

在这个问题上，我这种自己钟情于「折腾」笔记软件、又喜欢与别人分享折腾经历的人，似乎是一个「帮凶」。但我的本意绝非让大家把时间都花在摆弄设置上。今天这篇文章，我就不扯太多方法论，用一看就懂且有实践意义的 8 个用法去尝试解答 Obsidian 都能做到什么，并用尽量扼要的方式介绍步骤和操作。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-0df64631249766f301c1458952761d40-20221013060036-w0pohow.webp)

​

在介绍这些用法的过程中，我将穿插介绍数个常用插件。但篇幅有限，如果你对插件的进阶功能感兴趣，请阅读我一并贴出的开发者文档，或者期待我的下一篇文章吧。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-80fbafed43bc7c6f33db7ede39fd16c7-20221013060036-v28csg8.webp)

​

我个人很不习惯默认开启黑暗模式的设置，也不太喜欢自带的暗色主题。因此，建议安装后马上将笔记主题切换到明亮模式，或者尽快找到一款自己喜爱的第三方主题——只能说 Bear 和 Notion 会受欢迎是有原因的，颜值还真就是生产力。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-12748cae54b20ba82eb07c4f00b8f22c-20221013060036-kqj3pbr.webp)

​

如果你想要追求更好看的**原生排版体验**，也不喜欢折腾插件，我会更推荐思源笔记，同样支持本地离线 + 双向链接，这篇文章就是用思源笔记写的，请期待我的后续测评。

Obsidian 默认不开启 Daily Note 功能，Logseq 或 RoamResearch 用户可能会很不习惯，而对另一些没有接触过 Daily Note 概念的用户来说，也很有必要先介绍一下它的应用场景和配置方法。

## 什么时候记 Daily Note？

1.  当你想写日记的时候，它就是一个支持 Markdown 的日记本
2.  当你想快速记录灵感的时候，你不用也不该纠结应该放在哪个文件夹，就像传统纸笔，翻开就能写，就像摄影，拍到比拍好更重要。**而使用传统的笔记软件，你总要先找到（或建立）一个合适的文件夹用来存放**，但灵感和冲动往往消失在这个麻烦的时候。

## 配置方法

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/image-20221013061914169.png)

## 日记模板

一般来说我更习惯于用无序列表来让记录这件事更纯粹一点，模板对我来说会有填空的压力。但你也可以事先设置诸如晨间日记、每日工作等模板。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-9a161cd7dbe601edccdb0c103036e5b1-20221013060036-u5wcxri.webp)

​

设置好模板后，**使用快捷键**创建日记文档，就能自动调用这个模板，就像下图这样子：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-a7f4a7910db9da259af7fe6b93ee515f-20221013060036-rcvm5l5.gif)

​

当然你也可以让 Obsidian 在启动后，自动载入当天的日记页面，在 **设置** > **插件选项** > **日记** 中你可以找到这个选项。

## 日记进阶：双链入门

之所以能够随心所欲、不用分类地在 Daily Note 中记录一切内容，是因为有双向链接这个功能的托底。

点击每一个被 `[[]]`​ 框住的关键词，都会自动创建一个以这个关键词为名的文档，然后进入到这个文档中。比如在下图中我就通过这种方式创建了一个名为 `Notion`​ 的文档。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-5b98550fe2d4e0ccee0ab5baafc74870-20221013060036-c7qicvy.gif)

​

打开这个文档的反向链接面板，它会在笔记库内搜索**这个关键词曾经出现过的位置**：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-1cfb926503e75a0288b35e0b2908bccf-20221013060036-2scxtvi.gif)

​

所以我们用 Daily Note 记录那些不成主题的碎片信息，直到你有明确的专项题目可以拓展，再通过反链面板去回溯过去在 Daily Note 中留下的碎片记录，有时候靠那不经意的一句吐槽都能带来无穷的启发。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-f79182188f9e7cb7cf0bb97ad7caf001-20221013060036-l4pmjp5.webp)

​

## 日记进阶：初级任务管理

使用 Task 插件能用非常简单的语法，将分散于各篇日记的任务集中于一处管理，请在安装并启用 Task 插件后，执行如下操作

1.  在 **设置** > **快捷键** 中，搜索 **Tasks**，并为 **Task: Create or edit task** 创建一个快捷键命令，例如 `Ctrl+T`​；
2.  使用快捷键 `Ctrl+T`​ 唤出 Task 任务面板，然后在下图的自定义选项设置你的任务：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-d621a1a07389af5ff10dc229bcb60576-20221013060036-4nu6kwh.webp)

​

设置完毕后，你就可使用非常丰富的选项，来制定你的个性化任务面板，下面这段最简单的代码，能让你筛选出你**整个笔记库内所有未完成的任务。**

```
‍‍‍‍‍‍```task
```

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-80ee18a1f093bbe52a4a692802e5a851-20221013060036-cw6jfbn.webp)

​

你还可以参考开发者的这份[文档](https://eryinote.com/go?_=c529606e8daHR0cHM6Ly9zY2hlbWFyLmdpdGh1Yi5pby9vYnNpZGlhbi10YXNrcy9nZXR0aW5nLXN0YXJ0ZWQv)，制定更加个性化的任务面板，也可简单参考我下图中的命令。

## Day Planner 插件

Day Planner 与前文提到的 Tasks ，都能对笔记库中的 To-do 内容进行集中管理，Tasks 插件会更自由灵活，它能够扫描到笔记库内**任意地方**的 To-do 内容；而 **Day Planner 则只能扫描特定的文件夹**，但换来了更加精细、更加有趣的日程 / 任务管理方式，包括文档顶部自动生成甘特图、右侧自动生成时间线、底部右下角有全局的任务提示等。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-63b1a1ed1436f00fde7b8023a3a44715-20221013060036-4c9jks0.webp)

​

当任务到点时，还能弹出系统级的通知提醒：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-b183594bf388f3b6533b7d0608780b50-20221013060036-zrycl26.webp)

​

### 文档模式 File mode

安装完 Day Planner 插件后：

1.  会默认开启 File mode 功能；
2.  会在笔记列表根目录中自动创建名为 `Day Planner`​ 的文件夹；
3.  在 `Day Planner`​ 文件夹内，每天都会自动创建一个新的日程文件；
4.  你需要用下列语法格式来书写你的日程，才能被插件正确识别：

```
not done
```

几点提示：

*   你也可以使用 Ctrl+Enter 来快速创建 Checkbox
*   时间需要 24 小时制，1:00 应写成 01:00
*   时间与任务描述之间需要空格

如果右侧时间线没有正确显示，请使用下列操作：

*   使用快捷键 `Ctrl+P`​ 唤出命令面板；
*   搜索关键词 **show** ，然后选择 **Show the Day Planner Timeline**：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-a508683ec1197dd8f4483f187187741e-20221013060036-1gi4f8j.webp)

​

### 命令模式 Command mode

在插件设置中，将 File mode 切换到 Command mode，**能够让你在任意一页文档中使用 Day Planner 插件**，而无需创建额外的 Day Planner 文件夹。任务书写语法与 File mode 一样，但你还需要执行下面的操作:

1.  使用快捷键 `Ctrl+P`​ 唤出命令面板
2.  搜索关键词 `link`​ ，然后选择 `Link todays' Day Planner to the current note`​

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-e0da98370fc57a95799b27c292840870-20221013060036-eqdceza.webp)

​

## Kanban 插件

你可以像 Trello、Teambition、或者 Notion 中的 Board 面板 一样，去使用 Kanban 插件，它在常规看板的基础上，同样支持了双向链接功能，完整介绍你可以参考开发者这份[文档](https://eryinote.com/go?_=e349cf74afaHR0cHM6Ly9tYXR0aGV3bWV5ZS5ycy9vYnNpZGlhbi1rYW5iYW4v)。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-221902f09bc4d7e4b99d731d0852e207-20221013060036-7mhp43b.webp)

​

### **创建看板的两种方式**

1.  右键点击任意一个文件夹， 选择 **新看板**；
2.  `Ctrl+P`​ 唤出命令面板，搜索 **Kanban** ，并选择 **创建新看板**。

### **启用看板复选框**

**设置** > **插件选项** > **Kanban** 中，开启 **展示卡片复选框** 功能.

### **看板与双链联动**

为看板卡片添加时间，例如 `[[2022-03-24]]`​，当那天到来时，你就能在 24 号日记的**反向链接面板**看到这张卡片：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-7e3a454824631bc01291bc533d45e9b4-20221013060036-xh42757.webp)

​

每一张卡片都能创建为一份文档， 就像 Notion 中的 **/page** 命令 ，你只需要点击 **从卡片新建笔记** 即可。

工作最让我感到厌烦的，不是工作本身具有难度，而是每周、甚至每天都得形式化地写又臭又长、根本没有人看的工作报告，于是我用下面两个插件来尽可能地减轻这种痛苦：用 **Templater** 插件来创建自动化的模板，以及使用 **Dataview** 插件来让 Obsidian 拥有高级检索能力。

## Templater 插件

这个插件能让你在不同文件夹创建文档时，自动调用不同的模板。

例如在「日报」文件夹创建文档则调用「日报」模板，在「会议」文件夹则调用「会议记录」模板，它比 Notion 的 Template button 更便捷，比 Logseq 的 Template 的自定义程度更高，比印象笔记要加载半个世纪的模板库更是不知快到哪里去了。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-f095285179e5a68abc0747b86d1209f0-20221013060037-ngqplmi.webp)

​

### 插件配置

1.  你需要先建立一个专门用来存放模板的模板文件夹，并且提前写好你所需要的模板
2.  打开 **设置** > **插件选项** > **Templater**
    1.  在 **Template folder location** 将路径指向模板文件夹
    2.  打开 **Trigger Templater on new file creation** 这个选项
    3.  然后在 **Add New** 那一栏，将文件夹与模板一一对应。如下图所示，左边是文件夹，右边是模板文件。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-bba707d09330dd854bd8dd0fd5971bb4-20221013060037-5h97mzx.webp)

​

如此一来，当我们在 `会议记录`​ 文件夹新建文档，它创建的就不是空白文档，而是加载了模板的文档了。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-5d74b29ccd0031dfd3560381b1d65177-20221013060037-7j74gk2.gif)

​

你可能注意到了，上图调用模板生成文档时，还自动生成了时间 `2022-03-22`​，原因是我在模板中使用了 Templater 提供的时间变量，用法类似 Excel 中的 `=today()`​ 函数。

```
‍‍‍‍‍```
```

更多变量你可以参考阅读开发者的这份[文档](https://eryinote.com/go?_=660e5400faaHR0cHM6Ly9zaWxlbnR2b2lkMTMuZ2l0aHViLmlvL1RlbXBsYXRlci9pbnRyb2R1Y3Rpb24uaHRtbA%3D%3D)，活用变量和双链，你还可以在每天生成的日报中显示 `上一页`​ 和 `下一页`​ 的效果。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-b5e836cf418c2257506eef6340ce9ad3-20221013060037-o7smngw.gif)

​

这时你可能又会注意到，使用 Templater 插件创建的文档都叫 `未命名`​，那么有没有办法在创建文档的时候就自动使用当天的日期作为文档标题呢？答案是有的，你需要的那个插件叫 QuickAdd。

## QuickAdd 插件

这又是一个非常强大的插件， 不过今天我们只介绍它的四个功能之一：Template。它有两个特性，分别是为 Templater 插件的模板创建一个快捷键，而无需像之前那样通过右键文件夹来创建文档。另一个特性，则是让 Templater 插件创建文档时，让文档标题能以特定格式来自动生成，例如我们现在需要的「日期」。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-822542c36a22854f90ea859ffab6ba49-20221013060037-nkc2bzn.gif)

​

配置步骤上，首先，为 `创建日报`​ 添加一个 QuickAdd 动作：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-3cab4ab83f1baff7a8ee6238348e2dc7-20221013060037-1rhzx8a.webp)

​

然后，点击闪电图标，这样才能在命令面板（`Ctrl+P`​）中直接搜索到；再点击小齿轮， 进入详细配置界面：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-3d1c605794e224f7cbbc8beb6d6c58bb-20221013060037-dfql0dc.webp)

​

在这里我仅介绍了 QuickAdd 可能不到十分之一的功能用法，更多用法可以参考这份[开发者文档](https://eryinote.com/go?_=ab5816a4b4aHR0cHM6Ly9naXRodWIuY29tL2NoaG91bWFubi9xdWlja2FkZA%3D%3D)。

## Dataview 插件

假设现在到了周五临近下班的时间，我们需要**快速将 5 篇日报和 3 场会议记录整合成一篇周报**，如果是以前使用传统文档记录，我们可能需要**分别打开 8 个文件**，来回切换窗口，然后慢慢地将它们复制粘贴在一起，这真是一件既费心又烦人的事。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-b1446a2e0ddce5fe7eb0eb5c9a25a99c-20221013060037-cn4c99h.webp)

​

而同样的事情如果发生在 Obsidian 中，事情则会变得轻松不少。

如下图所示，当我在周报文件夹创建文档，触发了 Templater 的模板，而这个模板则用了 Dataview 语法进行了配置。我利用 Dataview 插件，自动汇总了过去一周的所有日报和会议记录：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-713136122b0b089f4e37950512c7bea9-20221013060037-m75ecvl.gif)

​

你可以 `Ctrl`​ + 鼠标左键点击 ，来打开同一份文档。左侧窗口使用 `Ctrl+E`​ 进入阅读视图，鼠标悬停在日报标题上方，通过弹出的小窗获取周报所需要的信息，然后就可以在右侧编辑视图下快速输入了。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-9e40ab0889f561bca740a5c82f0f48e1-20221013060037-fw29bey.gif)

​

### Dataview 配置方法

将下面这段代码放到 Templater 模板库中，然后命名为 `周报模板`​

然后再设置当 `在周报文件夹创建文档`​ ，则 `调用周报模板`​

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-fb14dae52dede984786e5edc6569b535-20221013060037-za5l228.webp)

​

但是你会发现，上面那段代码会汇总 `工作`​ 文件夹中的**所有文件**，因为我们还没添加过滤条件

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-dc4d537407d95838d4e47c7ee7a0205c-20221013060037-upkl33l.gif)

​

显然我们需要的只有那些创建时间在一周之内的日报和会议记录文档，所以我们还需要两个步骤

1.  为需要的文档打标签，分别是 `创建时间`​、`日报`​、以及 `会议记录`​
2.  让 Dataview 筛选过滤这些标签

### 用 YAML 语言为文档打标签

你可以在日报最开头手动输入下面的内容，**注意是英文输入法下的冒号，并且冒号后面需要空格**：

```
## 任务标题
```

也可以用 Templater 插件在创建日报文档时自动插入：

```
-[]07:00 任务
```

好了现在我们可以让 Dataview 插件正确过滤**创建时间在 7 日之内**，并且**包含日报标签**的文档了。

```
今天：<% tp.date.now("Do MMMM YYYY") %>
```

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-676b941239e27bb7982ceda162ca675f-20221013060037-4d5w4ib.gif)

​

后面，我还会反复提到这个插件，你可以自行阅读 [Dataview 插件开发者文档](https://eryinote.com/go?_=9a92854b94aHR0cHM6Ly9ibGFja3NtaXRoZ3UuZ2l0aHViLmlvL29ic2lkaWFuLWRhdGF2aWV3Lw%3D%3D)，学习更多高端操作，也可以点击下面大图，参考 Dataview 的部分语法。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-31d1b8c94d35dcc45313378d721429bf-20221013060037-1d7d6mg.webp)

​

## Annotator 插件

Obsidian 原生支持 PDF 阅读，你只需要将 PDF 文件**拖到文件夹上**即可载入，而安装 `Annotator 插件`​ 除了能让 Obsidian 额外支持阅读 EPUB 格式的文件，还能进行高亮、批注等操作。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-8684b65b8dd33de22fbd225d8d6eb1b0-20221013060037-eai8s6o.webp)

​

插件用法如下：

1.  将你的 PDF 文件拖入 Obsidian 的文件夹上
2.  新建一个文档，然后在文档的最开头添加下面这样的 YAML 语法

```
昨天：<% tp.date.yesterday("Do MMMM YYYY") %>
```

例如，如果我要打开存放在 `附件`​ 文件夹中的 `基督山伯爵.pdf`​，则正确的语法应该是

```
明天：<% tp.date.tomorrow("Do MMMM YYYY") %>
```

然后 `Ctrl+E`​ 进入阅读视图，如果无法正确读取 PDF 文档，可以点击右上角的三个小点，然后再点击 Annotate。

关于添加的批注，需要了解的是：

1.  所有高亮和批注都会成为侧边栏中的卡片
2.  点击卡片即可跳转回 PDF 原文位置
3.  你还可以为批注打上可被 Obsidian 识别的标签

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-66ee482a5c9e15f7d1ed4495d3114190-20221013060037-1bgyr4l.gif)

​

点击右上角的 **Open as MD** 关闭批注模式，然后进入阅读视图，你就能看到所有的高亮和批注都被搜集起来组成一篇文档了。

## Mindmap 插件

这个插件能够让文档的各级标题成为思维导图中的各个节点，并且导图中的各个节点也都是可以点击的。虽然导图的样式单一，且配色实在辣眼，但胜在简单易用。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-a736fcb042be87dec3a5a9506a91dca8-20221013060037-6h8al1u.gif)

​

这个用法本质上还是 Dataview 插件的另一种应用， 与前面的清单（list）不同，这次我们要绘制的是一张可以动态变化的表格（table）。假设我们为 4 本书分别写了 4 篇读后感，并在文档的最开头用 YAML 语法进行一点配置（打标签）。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-9df53cc40ac3de27cd2fe96776a74aaa-20221013060037-8qrgxvg.webp)

​

然后使用下面的 Dataview 语法进行配置：

```
从 Unsplash 随机载入一张图片：<% tp.web.random_picture() %>
```

其中：

*   `table`​ 定义的是 Dataview 的展现方式；
*   `table`​ 后面接的是你在 YAML 中打的标签；逗号要是英文输入状态；逗号后面接空格；
*   `from ""`​ 引号里的是你所要搜索的文件夹名称；
*   `sort`​ 这段，表示按照阅读时间这一项进行降序排列（descend）；
*   你也可以把阅读时间换成评分，把 `desc`​ 换成 `asc`​，这样一来就是按照评分进行升序排列了。

生成这样的表格效果如下图所示：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-3c8c07d4c0dcf2e20316e1d03bd43428-20221013060037-il74kw7.webp)

​

这个表格会动态更新，你写一篇，它就会自动增加一行：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-649a6f340ae7b1da211420d96d6f1c1e-20221013060038-gani0iz.gif)

​

你除了可以用前面反复提到的 Templater 插件来自动嵌入 YAML 标签，还可以搭配 QuickAdd 这个插件来进一步提高效率，这里就不展开讲解了。

作为一名新人 UP 主，我会特别注意视频中弹幕激增的节点，然后去分析这个 UP 主说了哪些话来激发观众发送弹幕的热情，很多看似 UP 主不经意的一句话，其实背后都能找到很多运营的门道。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-aa846715ba03b69e611cfef19e7c8c73-20221013060038-8uiln7h.webp)

​

B 站本身自带视频笔记功能，但只能说堪堪够用，回看笔记的入口很深，而且完全线上保存无法导出，好处是原生功能，打开即用无需折腾。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-1c8af064532ae821c4d77ec920f709dc-20221013060038-ks0psho.gif)

​

在 Obsidian 中，你可以这么操作：

1.  复制粘贴视频网址到 Obsidian 中；
2.  在阅读视图下，链接才能在 Obsidian 内部打开；
3.  在编辑视图下，才能通过右上角的五角星截取时间点。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-143a3a0d06ebef3e9c8c16f5e6631072-20221013060038-3d30q1r.gif)

​

## 案例：如何更有效地「骗」弹幕？

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-fe1b699cc0cfdfb8dd6d701431d4c19f-20221013060038-7rs92ko.webp)

​

如上图所示，我会使用 Media Extended 和 Media Extended Bilibili Plugin，将笔记和视频界面并列来学习其他 UP 主的视频。（如果这个插件无法正常启动，请先关闭 Annotator 这个插件，重启 Obsidian，再尝试启用。）

具体而言，通过内嵌的视频窗口，以及**点击即可回溯的时间节点**，能让我在复习这段话术时，更直观且更深刻地去学习这个 UP 主通过视频所能呈现出来的方方面面，**因为我不止要学习他说了什么，还要学习他是怎么说的**，学习他搭配了什么样的画面，语调的抑扬顿挫以及搭配的 BGM 节奏如何，而这种便捷的笔记 + 视频的呈现方式，是绝大多数只能单纯内嵌视频的软件所无法做到的。

例如，下面是我在看一个视频时记录的一些观察，供参考：

**话题质量够好**

*   话题本身很吸引人
*   话题和每个人息息相关
*   每个人都会存在不一样的情况
*   每个人都会好奇别人是什么样的情况
*   发弹幕无需思考成本

**引导方式合理**

*   **随机抽样：**没有针对性，不侵犯个人隐私
*   **常用三个软件：**无需成本，每个人不一样，可预见弹幕会很丰富，不会同质化刷屏
*   **我会在后台统计数据占比：**为用户提供发弹幕的意义，是有互动的，不是发完弹幕就没了
*   **看看是否符合我的猜测：**提供弹幕发完之后的期待感，或许可以增加关注

说实话，如果你有正经的数据分析工作，还是用正经的 Excel 或者其他专业软件来分析，此处仅用来展示 Obsidian 在数据呈现这块的可能性。

## 使用 Dataview 来聚合数据

以我的 B 站投稿为例，我将视频数据放在 YAML 表头，然后在正文记录运营相关的分析和复盘

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-9bf7c2fb30a34bc7bcba37c26b24d230-20221013060038-px8dyxw.webp)

​

然后就像前面提到的阅读清单，这张表格也是可以实时动态更新的。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-1a1993ade2e868cf5c23e4f6efc0b9bf-20221013060038-j4jhc6t.gif)

​

## 使用 Charts 让数据可视化

这个插件能够让你手动插入如下图所示的五种图表：

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-d46137ac4f453d8b5cc8bc96bd616259-20221013060038-gqlo1at.webp)

​

安装完插件后，使用 `Ctrl+P`​ 唤出命令菜单，然后搜索 charts 关键词，选择 Insert new Chart 即可，然后剩下的就是手动输入数据的基本操作了。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-6e064f6cf2cb5fb6e369301ac25c1476-20221013060038-oq09cnq.webp)

​

之所以叫「史迹」而不叫「史记」，是因为你除了可以用它来生成史料的时间轴，也能按照时间线来记录你的旅游足迹。

## Timelines 插件效果

你可以做一份投稿时间轴，也可以做一份游记时间轴，其实没有什么实际用处，但因为它能做，所以我就做啦。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-e3f8834aa48da3b5cf3226130f0a722b-20221013060038-3e6lmyn.webp)

​

除了竖轴，还有横轴可以选择。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-e5f590c053746b648a2b2927c70f6cfd-20221013060038-zta6ewb.webp)

​

### Timelines 插件配置方法

乍一看，配置时间轴的代码非常简单，只需要像下面这样，筛选出所有包含投稿标签的文章即可

首先是必不可少的还是用 YAML 语言打上几个标签，其中 `timeline`​ 标签是必须的，另一个标签则可由你自定义。你可能注意到了，我们可以在 `[]`​ 内一次性输入多个标签。

但这样做的前提是，我们需要在被筛选的文章内，先进行一点点配置。

然后还需要在**正文**中插入一段 HTML 代码，来定义时间轴中的文章封面、标题、时间等。

```
‍‍‍‍‍‍```dataview
```

如果你直接复制上面的代码，记得自行修改一下引号内的内容。其中我们需要修改的部分有 `date`​ 、`title`​ 、以及 `img`​ 这三项，否则时间轴的时间、标题和封面将无法正确显示。

![](https://mypicture-1257351426.cos.ap-beijing.myqcloud.com/net-img-48e4b4e58c92604e5fbd19be4a27faf3-20221013060038-e2k32q5.webp)

​

更多关于 Timelines 的教程，可以阅读插件作者的这份[文档](https://eryinote.com/go?_=355460fdebaHR0cHM6Ly9naXRodWIuY29tL0RhcmFrYWgvb2JzaWRpYW4tdGltZWxpbmVz)。

本文只能粗略展示 Obsidian 的简单用法。Obsidian 现在一共有 [523](https://eryinote.com/go?_=c9a860e7eaaHR0cHM6Ly9vYnNpZGlhbi5tZC9wbHVnaW5z) 个插件，我想应该没有什么需求是满足不了的。但还是要提醒一句，插件不求多，只要找到适合自己的那一两个就足够了。须知吾生有涯，而折腾也无涯，把更多时间花在创作上才是正道。

本文首发少数派：https://sspai.com/post/72385

**声明：**本站所有文章，如无特殊说明或标注，均为本站原创发布。任何个人或组织，在未征得本站同意时，禁止复制、盗用、采集、发布本站内容到任何网站、书籍等各类媒体平台。