---
title: Composer 项目如何获取 vendor 目录路径？
urlname: How-composer-get-vendor-directory
date: 2019-10-15 23:16:49
tags: 
- Composer
- Laravel-lang
- Validator
---
# 为什么

在使用 [illuminate\calidation](https://github.com/illuminate/validation) 这个包的时候，遇到了国际化的问题，我希望能够有各种语言的错误信息展示，但由于不是配合 [Laravel](https://github.com/laravel/laravel) 使用的，无法直接简答地设置语言，只能自己引入语言包。

<!--more-->

```
https://github.com/caouecs/Laravel-lang
```

这是一个收集了 73 种语言的项目，主要支持 Laravel 的各个子项目，其中就包括 Validation。

```
--vendor
  |--caouecs
  |  |--Laravel-lang
  |  |  |--src
  |  |  |  |--en
  |  |  |  |  |--validation.php
  |  |  |  |--zh-CN
  |  |  |  |  |--validation.php

```
这是我们看到的项目最终的目录，我需要定位的是 `validation.php` 文件的绝对路径，也就是说需要的是 `vendor` 的路径。

# 怎么办

查了一些资料，有人提供了一些有趣方法方法：
```
// 如果我们有 $composer 对象，可以直接获取
$composer->getConfig()->get('vendor-dir');
```

```
// 这个方法可以获取到 composer.json 文件
\Composer\Factory::getComposerFile();
```

```
// 通过 ReflectionClass 可以获取到 Composer 加载类的路径，然后获取 vendor 目录
$reflection = new \ReflectionClass(\Composer\Autoload\ClassLoader::class);
$vendorDir = dirname(dirname($reflection->getFileName()));
```