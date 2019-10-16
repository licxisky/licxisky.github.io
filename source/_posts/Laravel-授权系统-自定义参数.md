---
title: Laravel 授权系统 - 自定义参数
urlname: Laravel-authorization
date: 2018-06-25 10:32:42
tags:
- Laravel
- Policy
---
基础
==

本文基于 laravel 5.5  
在阅读本文前，请先浏览一下 [laravel 5.5 用户授权](https://laravel-china.org/docs/laravel/5.5/authorization/1310#methods-without-models)


<!--more-->


生成
==
```shell
php artisan make:policy PostPolicy --model=Post
```

我们用上面的命令生成的策略文件会含有四个方法（已去除所有注释）：

```php
<?php
namespace App\Policies;
use App\User;
use App\Models\Project;
use Illuminate\Auth\Access\HandlesAuthorization;
class ProjectPolicy
{
	public function view(User $user, Project $project)
	{
		//
	}
	public function create(User $user)
	{
		//
	}
	public function update(User $user, Project $project)
	{
		//
	}
	public function delete(User $user, Project $project)
	{
		//
	}
}
```

这四个方法对应的是 资源控制器的 CRUD 方案，也就是增、删、查、改。
我们一般会在控制器中使用：
```php
public function update(ProjectRequest $projectRequest, Project $project)
{
	$this->authorize('update', $project);
	...
}
```

当然，在策略方法名和控制器方法名一致时，有更加优美的写法（请参照 [laravel 5.2 用户授权 - 自动判断授权策略方法](https://laravel-china.org/docs/laravel/5.2/authorization/1113#f4021a) ）：
```php
public function update(ProjectRequest $projectRequest, Project $project)
{
	$this->authorize($project);
}
```
注：策略中的 `view` 对应的是 `show` 方法

自定义
===

很多时候，我们还得自己定义策略方法，一般情况与自动生成的方法无异，比如：

```php
public function foo(User $user, Project $project)
{
	//
}
```

但，如果方法的参数与策略对应的 `Model` 不一致，按照原有的方法使用会一直授权失败，403  
例：
一个部门（Department）有很多成员（User），项目（Project）属于部门，只有部门的成员可以创建项目
我们重写一下 `create` 方法，两个参数， User - 当前用户，Department - 项目属于的部门
```php
public function create(User $user, Department $department)
{
	//判断用户是否属于该部门
	return $department->users()->whereId($user->id)->exists();
}
```


我们要按照一下使用方法才能成功调用策略：

```php
public function create(Department $department)
{
	$this->authorize('create', [Project::class, $department]);
	// $this->authorize([Project::class, $department]);
}
```