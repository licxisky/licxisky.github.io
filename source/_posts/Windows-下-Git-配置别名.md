---
title: Windows 下 Git 配置别名
urlname: Windows-Git-alias
date: 2018-03-07 15:22:52
tags: 
- windows
- git
- linux
- bash
---
经常敲错 `Git` 命令？偶尔会感觉有些命令好长？`alias` 拯救你！


<!--more-->


作为一只程序猿，能坐着绝不站着，能躺着绝不坐着。那么设置别名的方法必须有（手动滑稽）。

Linux的命令行功能十分强大，百度一下都是方法，但 `Windows` 又该如何设置？

Git自带的别名设置
==========

这种方法百度一下也可以非常容易地找到，此处不单独列出，传送门：[http://blog.csdn.net/zhang31jian/article/details/41011313](http://blog.csdn.net/zhang31jian/article/details/41011313)

来自Linux的方法
==========

进入到Git Bash，输入`cd`，然后编辑 `.bashrc` 文件（没有则自己创建）

![GitBashWindows.png](/uploads/GitBashWindows.png "GitBashWindows.png")

按以下格式输入即可

![GitAliasWindows.png](/uploads/GitAliasWindows.png "GitAliasWindows.png")