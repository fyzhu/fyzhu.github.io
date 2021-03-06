---
title: shell快捷键
categories:
  - 未分类
date: 2021-09-08 15:19:32
tags:
---
下面列举一些经常使用的快捷键：

Ctrl + L 用于清理终端的内容，就是清屏的作用。其实 clear 命令也有同样效果，但是你不觉得 Ctrl + L 的按键比输入 clear 这五个字母更快速吗？
Ctrl + D 给终端传递 EOF （End Of File，文件结束符），在运行程序时很有用。有些程序我们需要在接收到 EOF 输入时结束，那么这个快捷键就可以派上用场了。比如我们之前演示过，退出 root 用户身份，就可以用 Ctrl + D。如果你在命令行提示符后什么也不输入的情况下直接按下这组快捷键，那么就会关闭当前的终端；
Shift + PgUp 用于向上滚屏，与鼠标的滚轮向上滚屏是一个效果；
Shift + PgDn 用于向下滚屏，与鼠标的滚轮向下滚屏是一个效果。
下面的快捷键在你编辑一条比较长的命令时很有用：

Ctrl + A 光标跳到一行命令的开头。一般来说，Home 键有相同的效果；
Ctrl + E 光标跳到一行命令的结尾。一般来说，End 键有相同的效果；。
Ctrl + U 删除所有在光标左侧的命令字符；
Ctrl + K 删除所有在光标右侧的命令字符；
Ctrl + W 删除光标左侧的一个“单词”，这里的“单词”指的是用空格隔开的一个字符串。例如 -a 就是一个“单词”；
Ctrl + Y 粘贴用 Ctrl + U、 Ctrl + K 或 Ctrl + W “删除”的字符串，有点像“剪切-粘贴”。


参考：
https://www.imooc.com/read/39/article/463