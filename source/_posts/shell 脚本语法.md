---
title: shell 脚本语法
date: 2017/08/02 14:53:43
tags: 
	- shell
categories: 
	- 编程
---

### 第一行必须是 **"#/bin/sh"**

* 它不是注释，"#!/bin/sh"是对shell的声明，说明你所用的是那种类型的shell及其路径所在；
* 如果没有声明，则脚本将在默认的shell中执行，默认shell是由用户所在的系统定义为执行shell脚本的shell.
* 如果脚本被编写为在Kornshell ksh中运行，而默认运行shell脚本的为C shell csh,则脚本在执行过程中很可能失败。
* 所以建议大家就把"#!/bin/sh"当成C 语言的main函数一样，写shell必须有，以使shell程序更严密。

<!-- more -->

### 注释

一行的开始是 `#`

### 变量

```
#/bin/sh
shell_name='demo'
echo $shell_name'.js' # 输出 demo.js
ehco $shell_name.js   # 输出 demo.js
cp shell_name.js copyed.js
```

**Tip: `=` 之间不能用空格隔开**

### 逻辑符号： `&&`, `||`

命令1 && 命令2

如果左边的命令成功了，执行右边的命令

命令1 || 命令2 

如果左边的命令失败了，执行右边的命令

### 接受参数

```
m=$1
n=$2
echo $m-$n
```

执行命令 `sh num.sh 3 9` ，输出 3+9

### 控制流： **if/then/elif/else/fi**

```
m='yes'
if [ "$m" == 'yes' ]; then
	echo 'yes'
elif [ "$m" == 'no' ]; then
	echo 'no'
else 
	echo 'both'
fi
```

**Tip: "[" "]" 前后要用空格隔开**

### 循环： **for/do/done**

```
str='hellow shell'
for loop in $str; do
	ehco $loop;
done
```

**Tip: 循环项是以空格拆分的字符串**

### 格式化输出时间

```
currentDate = "`date +%Y%m%d%H%M%S`"
echo $currentDate # 20170802153107
```

### exist

退出当前 `shell` 脚本，一般来说，返回0代表执行成功，其他值表示没有成功

```
exist 0 # 0
exist 1 # 1

1### 系统变量

pwd=$PWD	# 当前目录
user=$USER	# 当前用户
echo $pwd 	# /Users/aixieluo/Workspace/sh
echo $user 	# aixieluo

### 参考文档

[http://learn.akae.cn/media/ch31s0###html](http://learn.akae.cn/media/ch31s0###html)