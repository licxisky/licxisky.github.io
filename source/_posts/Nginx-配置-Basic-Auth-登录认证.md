---
title: Nginx 配置 Basic Auth 登录认证
urlname: Nginx-Basic-Authentication
date: 2020-04-04 16:59:42
tags: 
- Nginx
- Authentication
- Linux
---

简介
==
在HTTP中，基本认证（Basic access authentication）是一种用来允许网页浏览器或其他客户端程序在请求时提供用户名和口令形式的身份凭证的一种登录验证方式。


<!--more-->


优点
==

基本上所有流行的网页浏览器都支持基本认证。

缺点
==

虽然基本认证非常容易实现，但该方案创建在以下的假设的基础上，即：客户端和服务器主机之间的连接是安全可信的。特别是，如果没有使用SSL/TLS这样的传输层安全的协议，那么以明文传输的密钥和口令很容易被拦截。

该方案没有对服务器返回的信息提供保护。现存的浏览器保存认证信息直到标签页或浏览器被关闭，或者用户清除历史记录。HTTP没有为服务器提供一种方法指示客户端丢弃这些被缓存的密钥。这意味着服务器端在用户不关闭浏览器的情况下，并没有一种有效的方法来让用户注销。

用户名密码
==
Basic Auth 最简单的用户名密码是以文件的形式存在的
```bash
printf "name:$(openssl passwd -crypt password)\n" >> /path/to/your/password
```
将上面命令中的 `name` 和 `password` 替换为你需要的 `用户名` 和 `密码` 即可

Nginx 配置
==
Nginx 配置大致如下：
```
server {
    listen       80;   
    server_name  example.com;

    auth_basic   "登录认证";  
    auth_basic_user_file /path/to/your/password;
    autoindex on;

    root   /var/www;
    index  index.html index.php;
}
```

使用
==
```bash
# 浏览器中使用
直接在浏览器中输入地址, 会弹出用户密码输入框, 输入即可访问

# 使用 wget
wget --http-user=name --http-passwd=password http://example.com/xxx.zip

# 使用 curl
curl -u name:password -O http://example.com/xxx.zip
```