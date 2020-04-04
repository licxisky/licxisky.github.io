---
title: file_get_contents 知多少
urlname: how-much-do-you-know-about-file_get_contents
date: 2019-10-22 23:46:12
tags:
- PHP
- HTTP
- Curl
---

在使用 PHP 获取网络数据或者模拟网络请求时，我们有很多的选择，`file_get_contents($url)` 是比较方便的一种，我们通常会使用它来获取简单的 `GET` 链接，但是 `file_get_contents` 的功能其实非常强大。

<!--more-->

# 使用

- `file_get_contents` 可以模拟 `POST` 请求
- `file_get_contents` 可以设置 `header` 参数 
- `file_get_contents` 可以设置 `content` 参数 
- `file_get_contents` 可以设置 `timeout` 参数 


```
$opts = [
    'http' => [
        'method'  => 'POST',
        'header'  => "Content-Type: text/xml\r\n".
          "Authorization: Basic ".base64_encode ("$https_user:$https_password")."\r\n",
        'content' => $body,
        'timeout' => 60
    ]
];

$context = stream_context_create($opts);

$result = file_get_contents($url, false, $context);
```

# 比较

`file_get_contents` 这么全能，那它和 `curl` 比起来怎么样呢？

### 优点

- `file_get_contents` 使用更加简单便捷，对小白用户更加友好


### 缺点

- `file_get_contents` 性能在多次请求上，弱于 `curl`，原因是 `file_get_contents` 不缓存 `DNS`，不 `keeplive`。
- `file_get_contents` 不读取非 `200` 状态码的内容
