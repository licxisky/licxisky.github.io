---
title: 'Laravel 开发 Docker 容器部署（Windows and Linux） '
urlname: Laravel-docker
date: 2018-05-25 14:53:40
tags:
- windows
- linux
- Laravel
- docker
---
# 起
2013年发布至今， Docker 一直广受瞩目，被认为可能会改变软件行业。
很早就有接触过 Docker ，但由于种种原因，一直没进行过系统的部署。准备给实验室的学弟学妹系统的培训一下实验室的技术栈，就想到了 Docker


<!--more-->


# Docker
Docker 到底是什么以及一些相关的语法，请参考阮一峰老师的[Docker 入门教程][1]

# 相关
本文将会使用到

 1. Git
 2. Composer
 3. Docker
 4. Docker-compose

# Windows

 1. 下载 Docker for Windows
    [https://www.docker.com/docker-windows][2]
 2. 开启 Hyper-V 支持
    ![开启 Hyper-V][3] 
 3. 修改 Docker Hub 镜像地址
    ![修改镜像][4]
    中科大：[https://docker.mirrors.ustc.edu.cn][5]
 4. 设置共享磁盘（windows下的坑）
    ![共享磁盘][6]
    但一般而言，直接 Apply 是会失败的...
    这是由于 Windows 10 的共享文件夹权限的问题，总结了一下几种方案
    - [Docker for Windows 里的Shared Drives 设置不生效][7]
    - [Docker for Windows10 配置共享文件夹失败该如何解决?][8]
    - [win10系统，docker设置共享文件夹][9]
    - 我的方法
    在试过【1】和【3】后（充分条件）
       ![共享选项][10]
       ![专用][11]
       ![来宾][12]
       ![公用][13]
 5. 克隆 laradock 项目

    ```
    git clone https://github.com/Laradock/laradock.git
    ```

 6. 进入 `laradock` 目录将 `env-example` 重命名为 `.env`：

    ```cp env-example .env```
    
    ![配置文件][14]
    
    务必更改 Mysql 版本以及默认数据库，用户，不然可能导致错误

 7. 配置 `laradock/nginx/sites/default.conf`
    ![nginx 配置文件][15]

 8. 运行容器：

    ```
    docker-compose up -d nginx mysql
    ```
    第一次安装会消耗非常多的时间去 build ，请耐心等待

 9. 开发环境有 `workspace` 提供

    ```
    docker-compose up -d workspace
    ```
    `workspace` 将会安装 composer , git , nodejs , yarn 等软件
    ```
    docker-compose exec wroksapce bash
    ```
    进入容器
    ```
    exit
    ```
    退出容器

 10. 在 `laradock` 父目录下创建 `laravel` 项目

    ```
    composer create-project --prefer-dist laravel/laravel=5.5.* laravel
    ```

 11. 访问
    `laravel` 打开浏览器 `localhost`
    `mysql` `localhost`:`3306` `root` `root`

 

  [1]: https://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html
  [2]: https://www.docker.com/docker-windows
  [3]: https://upyun.lichaoxi.com/usr/uploads/2018/05/632317922.png
  [4]: https://upyun.lichaoxi.com/usr/uploads/2018/05/1935180986.png
  [5]: https://docker.mirrors.ustc.edu.cn
  [6]: https://upyun.lichaoxi.com/usr/uploads/2018/05/567958841.png
  [7]: https://blog.csdn.net/u012680857/article/details/77970351
  [8]: https://www.zhihu.com/question/57343529
  [9]: https://newsn.net/say/docker-share-folder.html
  [10]: https://upyun.lichaoxi.com/usr/uploads/2018/05/3578632474.png
  [11]: https://upyun.lichaoxi.com/usr/uploads/2018/05/4268348058.png
  [12]: https://upyun.lichaoxi.com/usr/uploads/2018/05/3433607195.png
  [13]: https://upyun.lichaoxi.com/usr/uploads/2018/05/2432682378.png
  [14]: https://upyun.lichaoxi.com/usr/uploads/2018/05/2316001407.png
  [15]: https://upyun.lichaoxi.com/usr/uploads/2018/05/2142791969.png