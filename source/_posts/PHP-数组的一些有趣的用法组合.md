---
title: PHP 数组的一些有趣的用法组合
urlname: Interesting-use-of-PHP-arrays
date: 2018-08-23 22:00:14
tags:
- PHP
- Array
---
最近对 PHP 原生的数组方法使用比较多，所以也积累了一些非常有趣的用法，本文中所有的代码都可以在 PHP7.* 的环境下运行
文章会不断更新，有问题欢迎评论

<!--more-->


# 获取数组最大值的键的集合
```php
$array = [
    'a' => 1,
    'b' => 2,
    'c' => 3,
    'd' => 3
];
$keys = array_keys($array, max($array));
echo json_encode($keys); // ["c","d"]

```
## 讲解
`max(array)` 方法会湖区数组中的最大值
`array_keys(array[, value = null])` 方法的第二个参数默认为 `null` ，为 `null` 时，方法返回第一个参数数组的所有键组成的数组；不为 `null` 时，返回第二个参数在第一个参数中的对应的全部键，返回结果为数组。

 