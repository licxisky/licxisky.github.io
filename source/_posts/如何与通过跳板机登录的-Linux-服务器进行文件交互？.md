---
title: 如何与通过跳板机登录的 Linux 服务器进行文件交互？
urlname: How-to-interact-with-Linux-server
date: 2019-10-16 23:15:58
tags:
- Linux
- Command
---
# 为什么

工作之后，面对的都是跳板机（堡垒机）作为中转的 Linux 服务器，公司禁止开放 FTP 或者类似的方法，但有时候又要上传或者下载文件。只能想找一种更加便捷安全的方法。

<!--more-->

# 怎么办

Lunix 和 Windows/Mac 可以通过 `rz`, `sz` 命令来进行 ZModem 文件传输。优点就是不用再开一个 sftp 工具登录上去上传下载文件。

sz：将选定的文件发送（send）到本地机器
rz：运行该命令会弹出一个文件选择窗口，从本地选择文件上传到 Linux 服务器

安装命令：
```
> yum install lrzsz
```
从服务端发送文件到客户端：
```
> sz filename
```
从客户端上传文件到服务端：
```
> rz
```
在弹出的框中选择文件，上传文件的用户和组是当前登录的用户

SecureCRT设置默认路径：

Options -> Session Options -> Terminal -> Xmodem/Zmodem ->Directories

Xshell设置默认路径：

右键会话 -> 属性 -> ZMODEM -> 接收文件夹