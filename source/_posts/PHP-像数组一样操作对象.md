---
title: PHP 像数组一样操作对象
urlname: PHP-array-object
date: 2018-10-08 16:04:31
tags:
- PHP
- Collection
- Extension
- Laravel
- Array
---
# Collection
Collection 是 Laravel 的一个集合类，它承接了 ORM 的结果输出，提供了大量的 PHP 自身并未提供的方法操作，同时还支持链式调用。

关于集合，[Laravel 官方文档][1]有专门的来讲 ，但 Collection 是一个内嵌的项目，并未单独独立出来，无法再其他场景下使用。有需求就有动力，有人讲之抽出单独开发了一个包 [Collect][2] ，甚至于有人开发出了 PHP拓展版 [Collection][3] 。

我也开发过 Collection 包以及 Collection 拓展，确实非常考验人的技术，对于相关的技术成长也有非常大的帮助。这篇文章并不是要讲 Collection , 而是由此延伸出的一些 PHP 使用技术点：如何像数组一样使用 Collection


<!--more-->


# 文档
http://note.youdao.com/noteshare?id=65c242d0b42fcdc3940e352bce302431
这是之前为自己开发的 Collection 写的一篇文档，我们可以像数组一样使用 

### 像使用数组一样使用 Collection

#### 使用 [] 操作键值
获取
```php
$collection = Collection::make([
    'name' => 'Lala',
    'age' => 2,
    'address' => 'Beijing',
    'friend' => [
        'name' => 'OFO',
        'age' => 3
    ]
]);

echo $collection['name']; // Lala
echo $collection['friend']['name']; // OFO
```
编辑
```php
$collection = Collection::make(['name' => 'Lala']);

$collection['name'] = 'Lala2';

// ['name' => 'Lala2'];

$collection['age'] = 2;

// ['name' => 'Lala2', 'age' => 2]
```
删除
```php
$collection = Collection::make(['name' => 'Lala']);

unset($collection['name']);

// []
```

#### 使用 foreach
```php

$collection = Collection::make([1,2,3,4,5,6]);

foreach($collection as $key => $value) {
    echo $key.$value;
}
// 011223344556
```

#### 使用 count 计算集合长度
```php

$collection = Collection::make([1,2,3,4,5,6]);

echo count($collection); // 6

```

#### 使用 json_encode
```php

$collection = Collection::make([1,2,3,4,5,6]);

echo json_encode($collection); // [1,2,3,4,5,6]

```
这样我们几乎可以不对以前的代码做任何修改即可引入新的工具包。

# 原理
http://php.net/manual/zh/reserved.interfaces.php
PHP中定义了几个接口，类似于迭代器模式，只要实现了这些接口就可以对对象执行以上操作。其实原理非常简单，实现也不麻烦，但很多时候，我们并不知道与这样一些接口，所以，学无止境。


  [1]: https://laravel-china.org/docs/laravel/5.6/collections/1388#available-methods
  [2]: https://laravel-news.com/use-collections-outside-laravel
  [3]: https://github.com/viest/php-ext-collection