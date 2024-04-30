## What Shell is Used For?

Windows10 useing PowerShell

## What Will Course Teach Us?

How to make the most of the tools, show you new tools to add to you toolbox.

## The Shell

### What is the Shell?

The shell is a programming environment.%%like Python or Ruby%%So it has variables, conditionals, loops, and functions.

Effect:

	To take full advantage of the tools your computer provides.

They allow you to run programs, give them input, and inspect theri output in a [[semi-structured]] way.

#### 不理解的知识

大多数的命令接受标记和选项（带有值的标记），它们以 `-` 开头，并可以改变程序的行为。

`ls -l` 参数可以更加详细地列出目录下文件或文件夹的信息

##### 在程序间创建连接

Shell 管道

`command1 | command2 `

`command1 | command2 [ | commandN… ]`

* 当在两个命令之间设置管道时，管道符 `|` 左边命令的输出就变成了右边命令的输入。只要第一个命令向标准输出写入，而第二个命令是从标准输入读取，那么这两个命令就可以形成一个管道。大部分的 Linux 命令都可以用来形成管道。
`这里需要注意，command1 必须有正确输出，而 command2 必须可以处理 command2 的输出结果；而且 command2 只能处理 command1 的正确输出结果，不能处理 command1 的错误信息。`

进程是什么?

根用户

时间戳是什么?

### ROOT USER

sudo 命令启用

1. 创建/读取/更新/删除系统中的任意文件
2. 不需要借助任何专用的工具, 轻松地配置系统内核

* 容易错误操作破坏系统

## SUMMAYP

How to make the most of the tools, show you new tools to add to you toolbox.

The shell effect:

* To take full advantage of the tools your computer provides.
