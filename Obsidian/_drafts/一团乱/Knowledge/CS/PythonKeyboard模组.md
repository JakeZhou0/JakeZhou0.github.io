## 特点

- 可以截获和处理所有的键盘事件，**全局事件钩子** (无论焦点在哪，都可以截获事件)
- 适用于 `Windows` 与 `Linux`（需要超级用户权限 ）也支持实验性的 `OS X`
- 纯 `Python`
- 支持 `Python 2` 和 `Python 3`
- 可以正确识别键盘上的按键，包括特殊字符和国际字符，可以适应不同键盘的布局。
- 测试和记录
- 鼠标的处理可以使用项目 [mouse](https://github.com/boppreh/mouse)（pip install mouse)

## 使用方法

安装 PyPI 包

````
pip install keyboard
````

或者克隆存储库 (不需要安装，源文件就足够了)

````
git clone https://github.com/boppreh/keyboard
````

或者 [下载并解压](https://github.com/boppreh/keyboard/archive/master.zip) 到您的项目文件夹中。

## 参考

- [boppreh/keyboard: Hook and simulate global keyboard events on Windows and Linux. (github.com)](https://github.com/boppreh/keyboard#keyboard.on_press)
