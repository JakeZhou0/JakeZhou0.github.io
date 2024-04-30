> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [community.codewave.163.com](https://community.codewave.163.com/CommunityParent/CommunityDetail?postsId=2760596124595200)

**GPT 出现后，对于低代码产品的影响、冲击一直是一个悬而未决的问题。事实上 GPT 不仅不会干掉低代码产品，还可以帮助低代码产品做得更好。本文会详细讲解 CodeWave 平台结合 AI 能力的思考与实践。**

![](https://community2.codewave.163.com:443/upload/app/image_acc0589f93ae4279887ddc7baa339a52_afaec238-82f5-4996-8fdd-0aae42f393de_efp5CPR1_20231212114216125.png)﻿﻿  

GPT 出现后，对于低代码产品的影响、冲击一直是一个悬而未决的问题。事实上 GPT 不仅不会干掉低代码产品，还可以帮助低代码产品做得更好。

最近开始梳理网易 CodeWave 智能开发平台平台的 AI 方向，本文会从产品技术角度详细聊聊 AI + 低代码结合的机会，以及 CodeWave 低代码平台如何通过 AI 能力，大幅降低低代码产品的开发门槛，提升产品竞争力的一些实践。

低代码的困境
------

低代码市场目前已经达到了 50 亿规模左右，并且以年 30% 的复合增长率高速增长，低代码产品也成了用户降本增效的重要选择之一。那对于市场上的诸多低代码产品，用户最看重什么呢？用户实际使用低代码产品的体验如何？

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)﻿﻿  

在我们的市场调研过程中发现，70% 的用户会把 " 用户体验 " 作为重要的关注方向，用户会深入关注低代码产品的交互、操作等，并且直接会作为自己决策的依据之一。

同时，45.3% 的企业用户觉得，目前采购的低代码平台并不好用，其中 70% 为中小型企业。

为什么会这样？说好的降本增效呢？我们来分析一下。

下面看这张图：

![](http://kms.fp.ps.netease.com/file/6553c871ac71d0ca486336fb6osLPiVC05)﻿﻿  

献丑了，这是 CodeWave 平台对接登陆的一个逻辑编排过程。我们可以看到需要做这样的一个登陆逻辑，需要对登陆的全流程、Http 基础知识、日志等功能模块、加密解密都非常熟悉，同时要熟悉低代码平台调用接口、赋值、设置 Header、打日志、解析数据等操作。一般来讲一个熟练的低代码教练可能要花费一天左右时间来完成这段逻辑的搭建，而对于一个完全不懂开发的人员来讲，他完全无法实现这块逻辑。

事实上，对于一个熟练的后端开发者来讲，用代码实现这段逻辑可能也就花费一个小时左右。这里暴露了低代码重要的一个问题：定制开发的使用门槛太高，效率太低。低代码产品进入到企业当中，首先要通过平台完成很多定制开发工作，以便跟企业自身 it 设施集成，这个过程一般通过低代码平台的逻辑编排或者流程编排能力，要求用户在熟悉编码能力的基础上使用平台进行搭建，其使用门槛相当高。

CodeWave 平台也经常会走进客户去了解客户实际的反馈。在一次调研中我们发现，逻辑编排这块反馈的问题非常多：

![](http://kms.fp.ps.netease.com/file/6553c88d709f315e64e8e74eGagEJqsi05)﻿﻿  

逻辑模块的问题中，最高频的问题问题逻辑阅读（69%），其次是逻辑编写（56%）

## 逻辑阅读​

- 在逻辑反馈问题中，超过 9 成用户反馈 " 复杂逻辑场景下，阅读之前的逻辑、他人的逻辑 " 遇到困难，• 在逻辑反馈问题中，约 3 成用户反馈 " 一个逻辑页面中承载的有效信息与我的预期有差距 "（信息密度问题）

## 逻辑编写​

- 最高频的三项问题依次是：复杂逻辑的编写和实现（78%）、逻辑调试（debug）（67%）、复杂应用大量逻辑的管理（56%）• 用户反馈的其他问题：对于系统提供的 create，update 等集成逻辑没有日志或者调试机制，一旦发生未知异常，就很难定位问题。

**所以，低代码在很多场景并不低。**

另外则是一个老生常谈的话题：质量问题。 低代码产品能做核心系统吗？大部分低代码产品并没有考虑性能、高可用、安全、可观测性等核心 Web 应用不可或缺的部分，同时搭建者的良莠不齐，也无法保证逻辑、sql 、数据建模的低代码部分设计合理，没有性能问题。拥有因此很多客户选择低代码产品，只会构建他们认为不太重要的一些内部管理系统、项目管理系统等。很多低代码仍然无法解决核心应用的搭建问题。

那么作为发展历史有几十年之久的低代码厂商，会坐以待毙吗？答案是不会的。目前的厂商逐步开始往以下这两块方向努力：​

- 提升效率，通过一定的机制让用户使用的门槛更低，使用更高效• 提升质量，使用户搭建的产品能够达到基本的开发工程师的质量要求，保证线上不出问题

而随着人工智能技术的发展，很多低代码厂商逐步尝试将人工智能技术引入，用于解决以上的两个问题。

低代码 & AI 业内发展
-------------

Mendix & Outsystem 作为世界老牌低代码厂商，2018 年就开始在自己的低代码平台中引入 AI 技术。Mendix 10 发布时，首次提出了 AI-ENHANCED APP DEVELOPMENT 概念。他们的主要思路为人工智能辅助开发（AIAD），他们会将下一代产品引入生成式人工智能（AIGC）。同时，生成式 AI 加入低代码和无代码开发平台，将会进一步降低使用低代码和无代码开发工具的门槛，并或将诞生新的智能开发技术。

![](http://kms.fp.ps.netease.com/file/6553c8deac71d0ca4863380aI283WkPq05)﻿﻿  

Mendix 的思路以 AI 辅助编程为主（[https://www.mendix.com/platform/ai/](https://www.mendix.com/platform/ai/)）。举例来讲，由于他们拥有一个强大的 IDE ，他们的 AI assist 能力首先考虑用户的编辑器体验。对于低代码编辑器使用者来讲，最头疼的就是如何在一大堆组件和逻辑中快速选择想要的了，所以 Mendix 从 IDE 的基本体验出发，参考代码补全和代码推荐的方式创造性地提出了节点推荐的方式:（如图所示）

![](http://kms.fp.ps.netease.com/file/6553c912ac71d0ca4863388fLivlc2s005)﻿﻿  

这种做法有效解决了 " 选择困难症 "。AI 会根据用户上下文计算推荐需要的内容，并计算权重用来排序，很类似搜索引擎的工作。同时类似的工作还有著名数据可视化平台 Tableau 的 Show Me 功能：

![](http://kms.fp.ps.netease.com/file/6553c926ac71d0ca486338dbQZYLDrp205)﻿﻿  

show me 则通过一系列的规则和数据类型的嗅探，智能的给用户提示需要的图表，有效的治疗了用户在数据可视化场景的 " 选择困难症 "。

对于后起之秀来讲，OutSystems 则从质量出发，推出了 OutSystems AI Mentor System

![](http://kms.fp.ps.netease.com/file/6553c940083aa5c236de4045rSIORc4y05)﻿﻿  

这个产品另辟蹊径，通过提示和改善用户搭建应用的质量，来提升低代码产品的可用性。

此类产品的思路更加贴近开发者，最重要的是能够有效的提升搭建出来产品的质量。AI Mentor System 会自动分析产品内的技术债务并给出优化建议，维度包括性能、安全、可维护性、架构设计等。同时产品会扫描目前的代码，判断里面是否会存在不合理性。

目前 CodeWave 产品 language server 的一些检查也属于此类。通过一系列的代码扫描和规则检测，能够有效避免用户搭建不合理的代码，构造不合理的架构，也利于企业 IT 能力的提升。

## D2C 技术的发展

由于在低代码搭建和日常编码中，前端的还原效率一直被诟病，D2C 技术在近几年也得到了长足的发展。通常的做法是解析设计稿中的 DSL 转换为代码，此种方式存在很多问题，比如边界条件的处理，需要手动标注等，因此一直没有得到大规模的应用。

![](http://kms.fp.ps.netease.com/file/6553cb72ab3783d2424d9c8dxcef5rmq05)﻿﻿  

2017 年论文 Pix2Code 首次提出使用深度学习技术实现 UI 截图生成 UI 结构描述，是人工智能技术结合前端的一次飞跃，也是首次 " 前端一丝论 " 的诞生。随之而来 2018 年微软 AI Lab 开源了草图转代码工具 Sketch2Code，2019 年阿里巴巴开源 Imgcook，都是端智能技术蓬勃发展的写照。

![](http://kms.fp.ps.netease.com/file/6553cb835a46cab6a3dc3dd5PBKjcOLZ05)﻿﻿

## 大模型的热潮：AIGC 技术

从 2022 年 3 月 openai 悄然 beta 他们的开放 api 开始，到 9 月份 Stable Diffusion 的横空出世，一直到 12 月 chatGPT 的发布，每个程序员都经历着日新月异的变革和是否会被代替掉的恐惧。

AIGC 技术的本质是通过自然语言交互增强原先的人机交互，主要解决各种场景的使用门槛高、容易出错、学习成本高的问题，因此 AIGC 主要分为以下的几个方向：

### 办公协同与内容创作

办公协同的代表作为 office copilot，以及国内做办公协同的 WPS、飞书、葡萄城等产品。此类产品通过自然语言驱动办公软件自动化生成产物，提升办公效率。内容创作的代表则是 Stable Diffusion、Jasper 等一众通过自然语言创造文本音视频的产品。这两类由于大家接触的很多，并且跟本文关系不大就不赘述了。重点讲讲另一块 AIGC 技术： AI 代码生成与智能体编程技术。

### AI 代码生成与智能体编程技术

AI 代码生成底层技术的代表代表为一众开源闭源代码大模型，国外代表为 Code llama，StarCoder 等，国内代表为 Codegeex，PanGu-Coder 等。此类技术竞争非常激烈，有官方的排名 (sota humaneval）。产品代表当然是我们耳熟能详的 Github copilot 以及网易的 Codemaker 了。

![](http://kms.fp.ps.netease.com/file/6553cba3ab3783d2424d9cc5ieRISqM705)﻿﻿

而智能体编程技术我们会在后面的 AI 架构部分详细展开，这个概念被大众所熟知来源于 6 月 23 日，OpenAI 专家提出了 《LLM Powered Autonomous Agents》概念，将智能体的通用架构明确阐述出来。LLM 并不是无所不能的。在这种情况下，以插件等形式对大语言模型进行能力拓展逐渐成为了一种有效形式。工具 / 插件的使用极大地拓宽了大语言模型的能力和应用边界。通常将 LLM 和工具的组合系统称为 " 智能体 "（又称 Language Agents）。

因此基于智能体的编程框架如火如荼的出现了，智能体内包含需求理解和一系列代码生成插件，通过 " 一句话需求 "，智能体框架就可以生成完整的可运行的全栈代码以及项目工程。智能体框架在 23 年得到了蓬勃发展，由于其借助一些 Prompt 技巧让 LLM 拥有了任务调度能力，从而产生了过于玄幻的效果，被称作 AGI (通用人工智能) 的前夜 [https://github.com/yzfly/Awesome-AGI-Agents](https://github.com/yzfly/Awesome-AGI-Agents)﻿

![](http://kms.fp.ps.netease.com/file/6553cbb5b1a132dd1a6e63edI7Hjb5Qu05)﻿﻿  

代码生成技术以及智能体编程技术出现后，" 程序员一丝 " 的言论又甚嚣尘上，很多人表示自己每天的工作就是靠 copilot 来 tab ，然后等着 xxxGPT 来干掉自己。作为 github copilot 的测试用户，copilot 工具确实大幅度提升了我糊业务的效率，因此很多人问，既然代码生成技术那么成熟，还需要低代码平台甚至程序员干什么呢？我是不是一句需求过去，整个软件能出来？（别笑，这就是客户的疑问和心声）

那 AI 代码生成或者 copilot 能力为什么不能代替低代码甚至程序员呢？我认为有以下几个原因：​

1. 程序设计语言是人用来指挥计算机干活的，是人与计算机的一种协议。自然语言是人类沟通的媒介，他的特点就是**模糊性**，很难精确跟需求幂等。而计算机语言才是程序精确运行的必要条件。想象一下，你如何用自然语言来描述以下的界面![](http://kms.fp.ps.netease.com/file/6553cbc78c1b8336031b090bDQ5g28rs05)﻿﻿  
2. 随着复杂度上升，软件开发已经不是单纯 coding 能够完成，需要通过组件、服务的封装以屏蔽细节。同时需要依赖业务背景知识的输入才能够构建。由于 AIGC 依赖大模型无记忆，**缺少现有 IT 资产和领域知识的输入**，很难在高度封装的基础上启动开发。

这个我们就不展开讲了，很容易理解，即使目前有 RAG 技术，也很难将领域知识或自己的代码仓库完全灌输给模型并让模型参考去生成我们想要的代码。代码生成技术通常只能生成那种比较底层的代码，很难按照我们的需求逐步封装，而这正是跟软件开发相悖的。

![](http://kms.fp.ps.netease.com/file/6553cbd85a46cab6a3dc3e9brcRJ8idM05)﻿﻿  

1. 一个需要稳定运行的系统需要很多的周边设施，如中间件、存储、运维等。AIGC 技术目前只能有限的解决一些代码生成问题。代码编写完就结束了吗，那肯定不是的，不信你看这张图：

![](http://kms.fp.ps.netease.com/file/6553cbead5c31d052661925bQwSxm8X605)﻿﻿  

1. 基于各类评测，AIGC 仍然难以完成复杂度高、专业度高的编码工作，甚至在一些简单场景的表现都较差。这里我们还是以事实说话，由于我之前做医疗的，我就问了他一些医疗的专业知识，回答当然是啼笑皆非的。同样回到刚才所讲的智能体技术，我们也可以从下图中某个开源智能体框架的评测中看到，只有少数简单的场景能够用智能体编程实现，稍微复杂点就完全无法实现了，评价为不如直接复制粘贴。

![](http://kms.fp.ps.netease.com/file/6553cc05d5c31d0526619299EUyRCccF05)﻿﻿  

事实上，构建一个软件从来都不是一个简单的事情。即使让一个 AI 来 " 写代码 "，也并不是一件简单的事情。我们看下图：

![](http://kms.fp.ps.netease.com/file/6553cc13d5c31d05266192c3WgzqrrTE05)﻿﻿  

以 Web 应用为例，用户需要学习 js/java 等基础语言，并在此基础上学习前端框架、后端框架、数据定义、数据查询以及流程引擎等框架、库、DSL 等。对于 AI 生成来讲，很难收敛技术，更别说精确到某种框架了。

究其原因**传统开发方式自由度过大，上下文复杂且不标准，概念太多，不利于 AI 构建能够收敛的应用**，往往用户第一次描述的需求是模糊和发散的，一次生成往往很难达到用户最终意图。同时由于 AIGC 的编码产品缺少所见即所得的能力，也很难让用户进行需求的更改。同时应用开发很复杂，从需求转换成应用本身需要设计很多模块，编码者需要具备的问题拆解和规划能力 AI 是很难具备的。同时做过代码生成模型训练的同学也会明白，开发场景不仅包括自有 IDE 知识，还包括用户导入的接口、扩展库和 SDK 等，知识众多，很难让 AI 完全学习。

那如果有什么机制或工具，既能够从语言层面保证 AI 生成代码的收敛和可维护性，又能借助现有的工具和库，还能完成应用从开发到上线托管的全流程，是不是能够解决问题呢？这便是 CodeWave 低代码平台 + AI 的实践。

CodeWave 的实践 NASL - 做 AI 友好的低代码设计
---------------------------------

**NASL** 是网易数帆 CodeWave 智能开发平台用于描述 Web 应用的领域特定语言。它主要包含两部分：基础语言和 Web 应用特定领域（如数据定义、数据查询、页面、流程、权限等）的子语言集合。他通过一套基础的语言系统（例如类型、常量变量、表达式等）支撑了各种 Web 应用的领域语言，做到了一套语言就可以描述 Web 应用开发的方方面面。

![](http://kms.fp.ps.netease.com/file/6553cc20d5c31d05266192e3RiGKYEKi05)﻿﻿  

基于这样的设计，我们只需要构建能够生产 NASL 的低代码平台，并将生成的 NASL 转换为应用实际运行时的 java 和 js 代码，就可以完成应用从开发到构建部署的全流程了。因此 CodeWave 提供了五个设计器专门来生产 NASL，并提供了 language server 能力做实时的类型检查，保证用户开发产物的质量，同时提供翻译器在发布阶段把 nasl 转换为 java 和 js 代码，产品架构如下：

![](http://kms.fp.ps.netease.com/file/6553cc30d5c31d0526619307S9i7aUay05)﻿﻿  

通过 Nasl 来定义编程语言，并以此设计低代码平台架构的优势，主要体现在三点：​

- 产品上限高。 能够通过丰富的表达能力来表达 Web 开发中的各种场景，包括页面、数据查询、逻辑、流程等，并且可以根据业务的需求定制翻译能力• 质量可控。尽可能减少专业概念的数量，通过类型检查、静态、动态分析和排错来降低用户写出低质量代码的可能性。•AI 友好。通过统一的 NASL 语言及可扩展的定义，可以方便的对大模型进行训练后让其生成，不需要让大模型生成各种语言框架，这点是 CodeWave 平台区别于其他低代码平台的重要因素：一颗大心脏。**只有架构本身对 AI 友好， 才能更好的结合 AIGC 能力。**

基于这样的架构设计，我们就推出了一系列的 AI 能力：

## NL2NASL - 自然语言生成 NASL

![](http://kms.fp.ps.netease.com/file/6553cc3ed5c31d0526619349yi5V1Chu05)﻿﻿  

我们很容易就能够发现，如果把原来的编辑器通过用户输入代替，就能够给低代码平台带来各类自然语言的辅助功能。因此我们直接规划了一系列的自然语言生成的场景：

![](http://kms.fp.ps.netease.com/file/6553cc7c1b59461177c83954R7qzIlgi05)﻿﻿  

根据之前调研的结果，我们优先上线了自然语言生成逻辑的功能。CodeWave 智能开发平台的开发者在使用低代码平台编写逻辑时，首先需要深入理解业务逻辑，并将其转化为可视化逻辑片段。他们需要能够高效、高质量地编写逻辑，避免操作复杂、重复编写的问题。有些开发者缺乏传统代码开发经验，因此逻辑开发上手门槛较高，难度较大。为了解决这个问题，我们提供开发辅助，降低逻辑编写门槛，帮助开发者快速上手，提高逻辑开发效率。

在技术调研时我们考虑了 LangChain 和 Agent 框架等，并确定了基于 LangChain（JS/TS 版）框架的方案。

整体架构如下（LogicChain）：

![](http://kms.fp.ps.netease.com/file/6553cc96ea15e24503cba9cehSEepNGC05)﻿﻿  

用户确认后的执行计划，与上下文生成的 ts 代码，再结合检索出的平台资产上下文（包括扩展逻辑和组件逻辑等），组装成 Prompt 传递给大语言模型。

大语言模型按限定要求生成 ts 代码，然后通过 ts2nasl 的 transformer 解析并转换成 nasl json 格式。再结合原来用户操作的上下文路径，在编辑器中组合执行。效果如下：

![](http://kms.fp.ps.netease.com/file/6553cca11b59461177c839960XYtW4lL05)﻿﻿  

自然语言生成逻辑功能的上线大幅度提高了逻辑编写的效率，降低了逻辑编写门槛。采用对话式操作流程，开发者可以在编写逻辑的过程中随时向 AI 助手提问，并通过多轮对话详细描述意图。AI 助手会分析开发者的意图并向开发者反馈，开发者可以根据分析内容选择是否执行，如果不执行，可以持续进行对话。AI 助手可以自由展开或收起，随时提问，随时开启新对话，并且支持同时在多个逻辑编辑页面上开启 AI 助手，高效辅助开发者进行逻辑编写。

简单重复的逻辑不再需要复杂繁琐的操作，生成的逻辑可复制拖动。对于复杂逻辑，开发者只需通过自然语言描述意图即可快速生成。生成的逻辑可以进行修改后使用。

## CodeWave AIGC 能力基座：智能体架构

随着大模型技术的发展，为了支撑日益膨胀的 AI 需求，不仅仅传统的人机界面交互会被颠覆，维持了很多年的存储 - 领域模型 - 服务端 - 客户端的应用架构也极有可能会被颠覆。我们迫切需要一个全新的架构来构筑 AI 应用，Agent 架构应运而生。

AI Agent 今年 4 月在开发者社区格外火热，AutoGPT 成为 Github 历史上涨星最快的项目。火热的背后是 Agent 的思路为我们带来了 Software 2.0 的图景：LLM 作为推理引擎能力不断增强，AI Agent 框架为其提供结构化思考的方法，软件生产进入 "3D 打印 " 时代，可以根据用户需求进行个性化定制，Agent 框架打造每个知识工作者信赖的 AI 工作伙伴。同时 6 月 23 日，OpenAI 专家提出了 《LLM Powered Autonomous Agents》概念（[https://lilianweng.github.io/posts/2023-06-23-agent/](https://lilianweng.github.io/posts/2023-06-23-agent/)﻿[）](https://lilianweng.github.io/posts/2023-06-23-agent/%EF%BC%89) 正式将 Agent 智能体架构搬上舞台。

![](http://kms.fp.ps.netease.com/file/6553ccb5ea15e24503cbaa1ckBvfO4iw05)﻿﻿  

**Agent 和早期的 LLM-based 应用相比，有几个显著差异点：​**

- 合作机制 orchestration：存在多模型、多 Agent 分工与交互的机制设计，能实现复杂的工作流。例如编程场景下可能有需求工程师 Agent 与编码工程师 Agent。• 与环境交互 grounding：Agent 能理解自己的不足，并适时从外部寻找合适的工具解决问题。例如目前很多 Agent 支持查询搜索引擎内容等。• 个性化记忆 memory：能记忆用户偏好和工作习惯，使用越久越了解用户。例如目前广泛使用的 RAG 技术来增强 LLM 的记忆能力• 主动决策 decision：Agent 有能力在虚拟环境中探索、试错、迭代。这个能力目前主要依赖 prompt 技巧，例如 cot/reAct/plan & solve 等。

由于低代码平台需要通过判断用户意图来确定采用哪块代码生成能力，因此我们也使用了 Agent 架构来构建我们的低代码平台，并进行了技术调研，包括提示工程（FewShot、CoT、ReAct、Agent 等技术）、LangChain 和 Agent 框架等，确定了基于 LangChain（JS/TS 版）框架的方案。

我们建立了一个对话式的需求分析智能体（AnalyzerAgent），通过这个 Agent 来判读用户的意图，并交给界面链（UIChain）或逻辑链（LogicChain）等，同时通过 nasl 语言转换的方式来精简 token，提高准确率。我们还通过向量数据库进行扩展库的知识缓存，支持扩展功能，解决 token 受限问题。

对话式的需求分析智能体架构如下：

![](http://kms.fp.ps.netease.com/file/6553ccf41304d64198b524bdHvkMhsyI05)﻿﻿  

用户的应用上下文和交互上下文通过 json2nasl2ts 转换成大语言模型能够识别的 ts 代码，如：

{ "concept":"IfStatement","label":" 条件分支 ","test": {…},"consequent": [ {…} ],"alternate": […] }

转换为

if (isNameDuplicated == true) { nasl.ui.showMessage(' 重复的角色名！'); } else { … }

结合经过反垃圾之后的聊天内容，再检索出历史经验，组装成 Prompt 传递给大语言模型。

大语言模型按照格式返回 { "plan":"…","text":"…","executable":"true/false" } 的 JSON 形式。 当 executable 为 true 时，为用户提供一个确认执行的按钮。

基于 Agent 架构，可以更好的识别用户意图，共享上下文和记忆，并提供 AI 应用的横向扩展能力，方便接入更多的 AI 能力。

## AI Coach-AI 编程教练

自然语言生成技术（AIGC）只是 AI 能力的一部分， 为了方便用户使用平台更好的搭建出高质量的应用，我们也提供了 **AICoach 能力。其中包括：**

### 解读能力

基于大模型与 NLG（自然语言生成）技术，对用户、平台生成的代码逻辑、可视化图表等进行解读，有效提升工作效率与团队协同效率。

CodeWave 智能开发平台的开发者往往是一个团队，他们需要编写逻辑同时也需要阅读他人编写的逻辑成果物，多人合作完成应用的开发。然而，阅读已有的逻辑成果物往往是一个难题，需要按照逻辑的联络一步一步阅读，费时费力，可能会出现获取错误信息的情况，从而无法有效支持逻辑的复用和协作开发，用各种优化方式（如折叠、注释等）效果也不大。因此，开发者需要能够快速、准确地阅读已有的逻辑，并将逻辑片段简要概括翻译，为其他开发者提供帮助。

![](http://kms.fp.ps.netease.com/file/6553cce5ea15e24503cbaa8eDcNrOScc05)﻿﻿  

灵感来源于原来做数据可视化使用的 NLG（自然语言生成技术），NLG 的一个很重要的应用就是解读这些数据，自动的输出结论和观点。

我们利用 GPT 的能力，设计了对话式逻辑解读方式，将低代码 DSL 语言转换成大语言模型熟悉的通用语言，提高准确率；采用分段解读技术，采取注释原来位置的方式，让大语言模型自行标记所在位置。用户的应用上下文和交互上下文通过 json2nasl2ts 转换成大语言模型能够识别的 ts 代码，其中会在逻辑块中标记原来 nasl 块的位置信息。

结合经过反垃圾之后的聊天内容，再检索出历史确认过的经验，组装成 Prompt 传递给大语言模型。

大语言模型按照格式返回 Array<{ "content":"…","jsonPath":"…" }> 的 JSON 形式。

当用户点击解读后的某块内容时，可以定位到可视化逻辑中的相应位置。

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)﻿﻿  

### 推荐能力

根据用户操作上下文指导用户后续工作，解决教练和用户在使用平台时 " 节点、组件太多了，我不知道该选择什么 " 这一类问题。

节点推荐目前有两条路线，一是通过统计分析的算法 N-gram 来驱动。

N-gram 是一种语言模型，他把文本中每一个字节片段称为 gram，对所有 gram 的出现频度进行统计，并且按照事先设定好的阈值进行过滤，形成关键 gram 列表，也就是这个文本的向量特征空间，列表中的每一种 gram 就是一个特征向量维度。该模型基于这样一种假设，第 N 个词的出现只与前面 N-1 个词相关，而与其它任何词都不相关，整句的概率就是各个词出现概率的乘积。这些概率可以通过直接从语料中统计 N 个词同时出现的次数得到。

由于我们整个逻辑节点是由 Nasl 节点来描述，所以可以通过 N-gram 对 Nasl 节点的预测来完成节点的推荐功能。

按照此思路， AI​ 团队对目前现有应用的逻辑节点进行了抽取，分析

- 一共有 11155 个工程 json 文件，从中抽样了 200 个文件进行隔离• 基于画布名称出现次数的统计，分别对每个工程文件中的所有画布进行了过滤

抽取策略举例：

![](http://kms.fp.ps.netease.com/file/655442903863c549ac270ab4cz4cyTJc05)﻿﻿  

经过调优最终达到了一个比较好的效果：

![](http://kms.fp.ps.netease.com/file/655442543863c549ac2708aeFNwt7UGp05)﻿﻿  

目前实现的效果如下：

![](http://kms.fp.ps.netease.com/file/6554311bb1fbf8ae60393311K8rTyJw305)﻿﻿  

但这条路线的问题在于，节点推荐只能推荐到节点粒度，对内部逻辑的实现无法推荐。也就是说如果用户选择了一个接口，你只能推荐到 " 数据处理 "，但没法直接把整个数据处理过程补全。因此会有第二个方案：

第二条路线是基于 nasl 的文本补全，类似 copilot 的补全能力。

![](http://kms.fp.ps.netease.com/file/655430e579edd60ebee875504Y5F7kBY05)﻿﻿  

由于 nasl 本身也是代码，因此如果将 nasl 交给代码模型进行学习，就有可能实现整段逻辑的补全，之后将补全逻辑转换为可视化节点即可。

但这个方案也有不少问题：

1. 用户在 WebIDE 进行可视化编程时，传给 LLM 的语言是什么？json 形式的 nasl ？文本化 nasl ？ts or java？

json 形式的 nasl 理论上太过庞大，token 容易超出限制，导致上下文不完全

文本化 nasl ，理论上需要建立一套文本化的 nasl 语法，并建立大量样本，给大模型学习，才有可能

借助于一门通用语言 nasl -> 通用语言 -> LLM -> recommend -> 词语法分析 > 通用语言 ast -> nasl ast

nasl 中有很多的领域 DSL，通用语言不认识：解决方案 -> 开发 edsl 函数库，建立映射关系

数据查询子领域本身 recommend：select * from student left join …

数据查询子领域与逻辑域结合 recommend：List students = select * from Student

流程子领域 recommend：流程图推荐

链路较长，本身 LLM 就不快，性能问题是个较大的挑战。需要建立实时编译 (nasl->sourcecode) 与反编译 (sourcecode->nasl) 的快速编译机制

此方案目前也在探索中。

### 架构优化能力

CodeWave 虽然是低代码平台，但用户仍然会通过平台搭建出难以维护的模块和应用。按照我们的梳理，用户的搭建产物可能影响系统稳定性的部分如下：

![](http://kms.fp.ps.netease.com/file/65542a85554d28fe7e7a1d6bj7qPl1b805)﻿﻿  

解决这类问题最先想到的便是静态代码分析方案，但由于平台本身内容均通过 NASL 去生成维护，传统的静态代码扫描方案（如 [SonarQube](https://github.com/SonarSource/sonar-java/blob/master/docs/CUSTOM_RULES_101.md)）并不能满足要求，因此低代码平台设计了一套基于 NASL 的代码分析引擎，架构如下：

![](http://kms.fp.ps.netease.com/file/655429abe2d91d9257d9be42bLpxMyF105)﻿﻿  

除了静态分析能够涵盖的内容，针对用户自定义编写的复杂逻辑，平台也会结合大模型的能力，让大模型给出适合的重构方案，其思路与 AI 逻辑解读类似，只是要求大模型返回其中不合理的设计和逻辑。

## Design2NASL - 设计稿转 NASL

D2C 技术本身在公司内的研究很多，如云音乐的海豹 D2C 就是非常优秀的平台能力。在此就不赘述了。但大模型能力大幅度发展的今天，传统 D2C 技术同样能够被大模型技术所增强。以下是 CodeWave 结合传统 D2C 技术的设计：

![](http://kms.fp.ps.netease.com/file/6554466824462517dc9b5278TqkqHXjf05)﻿﻿  

D2C 技术的本质是设计稿 / 图片的 schema 与代码的互相转换，最大的问题是页面布局排版的最佳实践，在编码侧和设计侧是完全不一样的，设计侧需要平铺，获取到的内容是在同一层级的，而在编码阶段（HTML+CSS），页面元素通常会有嵌套关系。一般 D2C 技术需要写很多的边界 Case 来处理这样的问题，例如：

![](http://kms.fp.ps.netease.com/file/6554472b863f04cab875f00embzjN4Du05)﻿﻿  

**区别于通常的 D2C 技术，CodeWave 这边会采用大模型能力对转换效果进行优化，由大模型来判断哪些元素在编码上需要进行分组。**

## RAG - 低代码文档检索增强

对于一个复杂的低代码产品来讲，文档是极为重要的，传统通过关键词进行搜索的文档不仅搜索命中率不高，搜索出来的内容也只能在单个文档中查看，若用户有跨场景的综合需求，传统的搜索能力就无法满足了。

为此我们也接入了 AI 部门 Chat Document 背后的服务，其原理为目前火热的 RAG 技术：

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)﻿﻿  

整个方案会将文档切片，向量化后存储到向量数据库。当用户搜索时会首先在向量数据库中查询相似度高的内容，之后将搜索出来的内容交给大模型去加工、总结，最后返回答案。这样不仅可以有效解决用户搜索的效率，也能够让用户更好地理解文档的内容。

![](http://kms.fp.ps.netease.com/file/65542c6e0d45983c0a8159ca9J1G32RW05)﻿﻿  

未来我们也会跟 AI 团队一起，推出企业私有化知识库的搭建解决方案，让每个企业都可以用低代码快速搭建自己的 copilot。

**CodeWave 低代码 + AI 产品核心原则**
----------------------------

在做低代码跟 AI 结合的基础上，为了保证用户的体验，避免 AI 能力的突兀，真正做到润物细无声，我们也总结了一系列的 AI

产品核心原则：

- 产品心智统一。Chat 类 AI 产品需要对话时的独立上下文，用户需要关注对话的交互操作。对于生产力工具，要避免 AI 功能与目前产品体验的使用割裂，做到无缝融入。• 降低操作门槛。生成式 AI 本质是基于自然语言的人机交互生产力产品，目标是帮助用户提升使用效率，如果 AI 能力的接入反而提升了用户的操作门槛，这类产品就失去了原本的意义了。• 推动最佳实践。AI 真正体现 " 智能化 "，不仅是通过大模型的 Zero shot 能力体现，还要跟目前产品自身的数据资产、技术资产积累结合起来，体现企业自身的技术优势。• 避免额外风险。AIGC 会出现产出物不受控、冗余、被用户绕过做其他用途等情况，因此在 AIGC 产品设计时要把控好边界，做好内容质量的检测，避免 AI 生成物影响系统的稳定性，出现更大的不可控因素。

未来
--

大模型能力的最大价值并不是各种 AIGC 能力，而是低门槛的 AI 服务化能力，我称之为 AI 下乡。随着大模型技术的发展，以后 AI 技能将向编程技能甚至生活技能发展，成为每个人都能理解且能够使用的技术底座。CodeWave 团队会始终跟进目前 AI 技术的发展，不断往产品中注入 AI 能力，让低代码产品变成 AI 的试验田，让低代码 + AI 这样的实践给用户更大的价值。

![](http://kms.fp.ps.netease.com/file/6553cd091304d64198b524ecZ0vVjsB105)
