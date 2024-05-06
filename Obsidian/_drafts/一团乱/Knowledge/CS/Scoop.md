## 什么是 Scoop

Scoop 是一款适用于 [[Windows]] 平台的 [[命令行]] 软件（包）管理工具，这里是 [Github介绍页](https://link.zhihu.com/?target=https%3A//github.com/ScoopInstaller/Scoop)。简单来说，就是可以通过命令行工具（[[PowerShell]]、[[CMD]] 等）实现软件（包）的安装管理等需求，**通过简单的一行代码实现软件的下载、安装、卸载、更新等操作**。其灵感来源于 [[macOS]] 的 [Homebrew](https://link.zhihu.com/?target=https%3A//github.com/Homebrew/brew)，[[Mac]] 用户可以去了解了解。

## 为什么使用 Scoop

在 Windows 下，搭建 [[开发环境]] 一直是一个复杂且困难的问题。由于没有一个统一的标准，导致各种开发环境的安装方式差异巨大，需要付出很多不必要的时间成本。而 Scoop 可以帮助你统一安装并管理常见的开发软件，省去了手动下载安装，配置环境变量等繁琐步骤。

例如安装 python 和 nodejs 只需要执行：

`scoop install python scoop install nodejs`

## 安装 Scoop

Scoop 需要 [Windows PowerShell 5.1](https://aka.ms/wmf5download) 或者 [PowerShell](https://aka.ms/powershell) 作为运行环境，如果你使用的是 [[Windows 10]] 及以上版本，Windows [[PowerShell]] 是内置在系统中的。而 Windows 7 内置的 Windows PowerShell 版本过于陈旧，你需要手动安装新版本的 PowerShell。

> 由于发现很多同学在设置 Windows 用户时使用了中文用户名，导致了用户目录也变成了中文名。如果按照 Scoop 的默认方式将软件安装到用户目录下，可能会造成部分软件执行错误。所以这里推荐安装到自定义目录，如果需要其他安装方式请参考： [ScoopInstaller/Install](https://github.com/ScoopInstaller/Install)

`# 设置 PowerShell 执行策略 Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser # 下载安装脚本 irm get.scoop.sh -outfile 'install.ps1' # 执行安装, --ScoopDir 参数指定 Scoop 安装路径 .\install.ps1 -ScoopDir 'C:\Scoop'`

## 使用 Scoop

Scoop 的官方文档对于新手非常友好，相对于在此处赘述更推荐阅读 [官方文档](https://github.com/ScoopInstaller/Scoop) 或 [快速入门](https://github.com/ScoopInstaller/Scoop/wiki/Quick-Start) 。

## Q&A

### Scoop 能配置镜像源吗？

Scoop 社区仅维护安装配置，所有的软件都是从该软件官方提供的下载链接进行下载，所以无法提供镜像源。如果因为你的网络环境导致多次下载失败，那么你需要一点点 [魔法](https://csdiy.wiki/%E5%BF%85%E5%AD%A6%E5%B7%A5%E5%85%B7/%E7%BF%BB%E5%A2%99/)。

### 为什么找不到 Java8？

原因同上，官方已不再提供 Java8 的下载链接，推荐使用 [ojdkbuild8](https://github.com/ScoopInstaller/Java/blob/master/bucket/ojdkbuild8.json) 替代。

### 我需要安装 Python2 该如何操作？

对于已经过时弃用的软件，Scoop 社区会将其从 [ScoopInstaller/Main](https://github.com/ScoopInstaller/Main) 中移除并将其添加到 [ScoopInstaller/Versions](https://github.com/ScoopInstaller/Versions) 中。如果你需要这些软件的话需要手动添加 [[bucket]]：

`scoop bucket add version scoop install python27`
