---
title: 如何提升PHP性能？
urlname: How-to-improve-the-performance-of-PHP
date: 2018-05-09 03:28:20
tags:
- PHP
- 性能
---
最近遇到了一些程序性能相关的问题，在这里简单记录一下

世界上最好的语言
========

换 PHP7.1 吧，不然谈什么性能


<!--more-->


代码层次
====

1.  用单引号来包含字符串要比双引号来包含字符串更快一些。因为PHP会在双引号包围的字符串中搜寻变量，单引号则不会。
2.  如果能将类的方法定义成`static`，就尽量定义成`static`，它的速度会提升将近4倍。
3.  `$row['id']` 的速度是 `$row[id]` 的7倍。
4.  `echo` 比 `print` 快，并且使用 `echo` 的多重参数(译注：指用逗号而不是句点)代替字符串连接，比如 `echo $str1,$str2`。
5.  在执行`for`循环之前确定最大循环数，不要每循环一次都计算最大值，最好运用`foreach`代替。
6.  注销那些不用的变量尤其是大数组，以便释放内存。
7.  尽量避免使用`__get`，`__set`，`__autoload`。
8.  `require_once()`代价昂贵。
9.  `include`文件时尽量使用绝对路径，因为它避免了PHP去`include_path`里查找文件的速度，解析操作系统路径所需的时间会更少。
10.  如果你想知道脚本开始执行(译注：即服务器端收到客户端请求)的时刻，使用`$_SERVER[‘REQUEST_TIME']`要好于`time()`。
11.  函数代替正则表达式完成相同功能。
12.  `str_replace`函数比`preg_replace`函数快，但`strtr`函数的效率是`str_replace`函数的四倍。
13.  如果一个字符串替换函数，可接受数组或字符作为参数，并且参数长度不太长，那么可以考虑额外写一段替换代码，使得每次传递参数是一个字符，而不是只写一行代码接受数组作为查询和替换的参数。
14.  使用选择分支语句(译注：即`switch case`)好于使用多个`if，else if`语句。
15.  用`@`屏蔽错误消息的做法非常低效，极其低效。
16.  打开`apache`的`mod_deflate`模块，可以提高网页的浏览速度。
17.  数据库连接当使用完毕时应关掉，不要用长连接。
18.  错误消息代价昂贵。
19.  在方法中递增局部变量，速度是最快的。几乎与在函数中调用局部变量的速度相当。
20.  递增一个全局变量要比递增一个局部变量慢2倍。
21.  递增一个对象属性(如：`$this->prop++`)要比递增一个局部变量慢3倍。

应用层次
====

1.  Redis
2.  Swoole
3.  数据库连接池
4.  opcache
5.  HHVM

总结
==

PHP已经很快了，但是还可以更快，想想Facebook，再想想你的小项目  
平时多注意注意这方面的讯息，说不定哪天就用到了呢...