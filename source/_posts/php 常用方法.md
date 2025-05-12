---
title: php 常用方法
date: 2017/09/08 11:41:27
tags: 
	- function
categories: 
	- 编程
---

记录一些常用的 PHP 基本方法

<!-- more -->

## 数组相关

### `array_merge_recursive(array1 [, array2] [...])` 把一个或者多个数组合并成一个数组

```php
$a = ['a' => 1, 'b' => 2];
$b = ['b' => 3, 'c' => 4];
array_merge_recursive($a, $b);
// ['a' => 1, 'b' => [0 => 2, 1=> 3], 'c' => 4]
```

### `array_keys(array [, value] [, strict])` 返回包含数组的所有键名的一个新数组

```php
$arr = ['a' => 'b', 'c' => 'd'];
array_keys($arr);
// ['0' => 'a', '1' => 'c']
```

### `array_search(value, array [, strict])` 在数组中根据键值返回对应键名

```php
$arr = ['a' => 'red', 'b' => 'yellow'];
array_search('red', $arr);
// 'a'
array_search('black', $arr);
// false
```

### `array_push(array, value [, value2])` 给数组尾部添加一个或者多个新元素

```php
$arr = ['0' => 'a', '1' => 'b'];
array_push($arr, 'c', 'd');
// ['0' => 'a', '1' => 'b', '2' => 'c', '3' => 'd']
```

### `array_flip($array)` 用于交换数组的键名和其对应的键值

```php
$arr = [0 => 'a', 1 => 'b'];
array_flip($arr)
// ['a' => 0, 'b' => 1]
```

## 字符串相关

### `strpos(string, find [, start])` 查找一个字符串在另一个字符串中第一次出现的位置（对大小写敏感）

```PHP
echo strpos("You love php, I love php too!","php");
//9
```

## IO相关

### `is_file(file)` 检查指定文件名的文件是否是正常的文件

本函数的结果会被缓存，请使用 `clearstatcache()` 来清除缓存

```PHP
is_file($path)
// true 
```

## 时间相关

### `strtotime(time, now)` 将任何英文文本的时间或者日期转换为unix时间戳

```PHP
echo(strtotime("now") . "<br>");
echo(strtotime("5 September 2016") . "<br>");
echo(strtotime("+5 hours") . "<br>");
echo(strtotime("+1 week") . "<br>");
echo(strtotime("+1 week 3 days 7 hours 5 seconds") . "<br>");
echo(strtotime("next Monday") . "<br>");
echo(strtotime("last Sunday"));
//1505185265
//1473004800
//1505203265
//1505790065
//1506074470
//1505664000
//1504972800
```
