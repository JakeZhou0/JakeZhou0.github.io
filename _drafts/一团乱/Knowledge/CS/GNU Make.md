## **什么是 GNU Make?**

GNU Make 是一个可以自动运行 [[shell]] 命令并帮助执行重复任务的 [[程序]]。它通常用于将文件转换成其他形式，例如将源代码文件编译成程序或库。

它通过跟踪先决条件和执行命令层次结构来生成目标来实现这一点。

尽管 GNU Make 手册很长，但我建议阅读一下，因为它是我找到的最好的参考:[https://www.gnu.org/software/make/m](https://link.zhihu.com/?target=https%3A//www.gnu.org/software/make/manual/html_node/index.html)

## 为什么学 GNU Make

大家第一次写 hello world 程序的时候一定都记得，在编辑完 `helloworld.c` 之后，需要用 `gcc` 编译生成可执行文件，然后再执行（如果你不理解前面这段话，请先自行谷歌 _gcc 编译_ 并理解相关内容）。但如果你的项目由成百上千个 C 源文件组成，并且星罗棋布在各个子目录下，你该如何将它们编译链接到一起呢？假如你的项目编译一次需要半个小时（大型项目相当常见），而你只修改了一个分号，是不是还需要再等半个小时呢？

这时候 GNU Make 就闪亮登场了，它能让你在一个脚本里（即所谓的 `Makefile`）定义整个编译流程以及各个目标文件与源文件之间的依赖关系，并且只重新编译你的修改会影响到的部分，从而降低编译的时间。

## 如何学习 GNU Make

这里有一篇写得深入浅出的 [文档](https://seisman.github.io/how-to-write-makefile/overview.html) 供大家参考。

GNU Make 掌握起来相对容易，但用好它需要不断的练习。将它融入到自己的日常开发中，勤于学习和模仿其他优秀开源项目里的 `Makefile` 的写法，总结出适合自己的 template，久而久之，你对 GNU Make 的使用会愈加纯熟。
