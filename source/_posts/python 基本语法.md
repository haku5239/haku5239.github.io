---
title: python 基本语法
date: 2017/11/22 17:05:38
tags: 
	- python
categories: 
	- python
---

python 基础语法入门

<!-- more -->

### 数据类型

#### 1.整数

> `1`, `100`, `-10`

#### 2.浮点数

> `3.14`, `-.9`, 对于很大或者很小的浮点数，采用科学计数法表示，`1.23e9`, `12.3e8`
> 整数和浮点数在计算机内部存储的方式是不同的，整数运算永远是精确的（除法难道也是精确的？是的！），而浮点数运算则可能会有四舍五入的误差。

#### 3.字符串

> 字符串是以''或""括起来的任意文本，比如'abc'，"xyz"等等。
> 请注意，''或""本身只是一种表示方式，不是字符串的一部分，因此，字符串'abc'只有a，b，c这3个字符。

#### 4.布尔值

> `True`, `False` （请注意大小写）
> 布尔值可以用and、or和not运算。

#### 5.空值

> 空值是Python里一个特殊的值，用 `None` 表示。`None` 不能理解为0，因为0是有意义的，而 `None` 是一个特殊的空值。

### print语句

```
>>> print 300
300    #运行结果
>>> print 100 + 200
300    #运行结果
>>> print '100 + 200 =', 100 + 200
100 + 200 = 300     #运行结果
```

### 注释

> Python的注释以 `#` 开头，后面的文字直到行尾都算注释

### 变量

> 在Python程序中，变量是用一个变量名表示，变量名必须是<strong> `大小写英文`、 `数字` 和 `下划线` 的组合，且不能用数字开头<strong>

### 字符串

> `Hello, World!`
> 如果字符串既包含 `'` 又包含 `"`, 则需要对字符串的某些特殊字符进行 `转义`
> 常用转义字符
> \n 表示换行
> \t 表示一个制表符
> \\ 表示 \ 字符本身

### Raw字符串与多行字符串

#### Raw字符串

> `r'...'`
> Raw字符串内部不需要转义
> 但是 `r'...'` 表示法不能表示多行字符串，也不能表示包含 `'` 和 `"` 的字符串

#### 多行字符串

```
'''Line1
Line2
Line3'''
# 与下面字符串意义相同
'Line1\nLine2\nLine3'
```

> r'''...'''
> 在多行字符串前面添加 `r` ，把这个多行字符串也变成一个raw字符串

### Unicode字符串

> 如果中文字符串在Python环境下遇到 UnicodeDecodeError，这是因为.py文件保存的格式有问题。
> 可以在第一行添加注释
> `# -*- coding: utf-8 -*-`
> 目的是告诉Python解释器，用UTF-8编码读取源代码。

### 列表list

> list是一种有序的集合，可以随时添加和删除其中的元素。
> list是数学意义上的有序集合，也就是说，list中的元素是按照顺序排列的。
> list的索引从0开始
> 索引可以倒序访问list
> 使用索引越界时，会报错 `IndexError: list index out of range`
> 添加新元素时使用方法 `append()`, 会把新元素追加到list的末尾
> 也可以使用方法 `insert()`, `insert()` 接受两个参数，第一个是索引号，第二个是待追加的新元素
> 删除元素使用方法 `pop()`, 接受一个参数，索引号
> 替换元素可以直接使用索引号重新赋值

```
L = ['a', 'b', 'c']
L[0] # 'a'
L[-1] # 'c'
L.append('d')# ['a', 'b', 'c', 'd']
L.insert(1, 'A') # ['a', 'A', 'b', 'c', 'd']
L.pop(1) # ['a', 'b', 'c', 'd']
L[0] = 'A' # ['A', 'b', 'c', 'd']
```

### 元组tuple

> tuple是另一种有序的列表，中文翻译为“ 元组 ”。tuple 和 list 非常类似，但是，tuple一旦创建完毕，就不能修改了。
> 创建tuple和创建list唯一不同之处是用 `( )` 替代了 `[ ]`。
> 因为 `()` 既可以表示tuple，又可以作为括号表示运算时的优先级，所以Python规定单个元素的tuple，需要多加一个 `,`, 例如 `(1,)`, 这样就避免了歧义

```
T = (1, 2, 3, 4, 5)
T = (1, 2, [3, 4]) # 此时T中的list为可变，所以tuple也“可变”了
```

### 条件判断语句

#### if

```
if True:
	print 'success'
```

#### if-else

```
if True:
	print 'success'
else:
	print 'error'
```

#### if-elif-else

```
n = 1
if n == 1:
	print n
elif n == 2:
	print n
else
	print 'error'
```

#### for循环

```
L = ['Adam', 'Lisa', 'Bart']
for name in L:
    print name
```

#### while循环

```
N = 10
x = 0
while x < N:
    print x
    x = x + 1
```

#### break

> 用 for 循环或者 while 循环时，如果要在循环体内直接退出循环，可以使用 break 语句。

#### continue

> 在循环过程中，可以用break退出当前循环，还可以用continue跳过后续循环代码，继续下一次循环。

### dict

#### 介绍

> 花括号 {} 表示这是一个dict，然后按照 key: value, 写出来即可。最后一个 key: value 的逗号可以省略。
> 由于dict也是集合，len() 函数可以计算任意集合的大小，一个 key-value 算一个
> dict的第一个特点是查找速度快，无论dict有10个元素还是10万个元素，查找速度都一样。而list的查找速度随着元素增加而逐渐下降。
> 不过dict的查找速度快不是没有代价的，dict的缺点是占用内存大，还会浪费很多内容，list正好相反，占用内存小，但是查找速度慢。
> 由于dict是按 key 查找，所以，在一个dict中，key不能重复。
> dict的第二个特点就是存储的key-value序对是没有顺序的！
> dict的第三个特点是作为 key 的元素必须不可变，Python的基本类型如字符串、整数、浮点数都是不可变的，都可以作为 key。但是list是可变的，就不能作为 key。

```
d = {
    'Adam': 95,
    'Lisa': 85,
    'Bart': 59
}
```

#### 访问dict

```
# 方式1
d['Adam']
# 方式2
d.get('Adam')
```

#### 更新dict

```
d['Adam'] = 90
```

#### 遍历dict

```
for k in d:
	print k
# Lisa
# Adam
# Bart
```

### set

#### 介绍

> set 持有一系列元素，这一点和 list 很像，但是set的元素没有重复，而且是无序的，这点和 dict 的 key很像。
> 创建 set 的方式是调用 set() 并传入一个 list，list的元素将作为set的元素。
> 因为set不能包含重复的元素，所以，当我们传入包含重复元素的 list时，set会自动去掉重复的元素。

```
s = set(['A', 'B', 'C'])
```

#### 访问set

> 由于set存储的是无序集合，所以我们没法通过索引来访问.
> 访问 set中的某个元素实际上就是判断一个元素是否在set中。

```
'A' in s # True
'D' in s # False
```

#### 特点

> set的内部结构和dict很像，唯一区别是不存储value，因此，判断一个元素是否在set中速度很快。
> set存储的元素和dict的key类似，必须是不变对象，因此，任何可变对象是不能放入set中的。

#### 遍历set

> 由于 set 也是一个集合，所以，遍历 set 和遍历 list 类似，都可以通过 for 循环实现。

#### 更新set

> 由于set存储的是一组不重复的无序元素，因此，更新set主要做两件事：
> 一是把新的元素添加到set中，二是把已有元素从set中删除。
> 添加元素时，用set的add()方法，如果添加的元素已经存在于set中，add()不会报错，但是不会加进去了。
> 删除set中的元素时，用set的remove()方法，如果删除的元素不存在set中，remove()会报错。
> 所以用add()可以直接添加，而remove()前需要判断。

```
s.add('A') # set(['A', 'B', 'C'])
s.remove('A') # set(['B', 'C'])
```

### 函数

#### 介绍

> Python内置了很多函数，我们可以直接调用。
> 可以直接从Python的官方网站查看文档：[Python函数](http://docs.python.org/2/library/functions.html)

#### 自定义函数

> 在Python中，定义一个函数要使用 def 语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用 return 语句返回。
> 函数还可以返回多个返回值
> 在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。

```
def my_fn(name, age):
	return name, age
name, age = my_fn('A', 20) # name='A' age=20
```

#### 定义默认参数

```
def my_fn(name='A'):
	return name
my_fn() # 'A'
```

#### 定义可变参数

> 可变参数的名字前面有个 * 号，我们可以传入0个、1个或多个参数给可变参数
> 可变参数也不是很神秘，Python解释器会把传入的一组参数组装成一个tuple传递给可变参数，因此，在函数内部，直接把变量 args 看成一个 tuple 就好了。

```
def fn(*args):
	print args
```

### 切片

#### 正序切片

> `L[x:y:z]` 如例所示，L是一个list，x，y代表索引号（x包含本身，y不包含本身），z代表间隔数
> 如果x是0，还可以省略
> 如果一直取到最后一位，则y省略
> z默认为1，省略不写

```
L = [1, 2, 3, 4]
L[:] # 从开始取到最后一个，也就是一个完整的新的list
L[:2] # [1, 2]
L[1:] # [2, 3, 4]
L[::2] # [1, 3]
```

#### 倒序切片

> Python支持L[-1]取倒数第一个元素，那么它同样支持倒数切片
> 倒数第一个元素的索引是-1。倒序切片包含起始索引，不包含结束索引。

```
L[-4:-1] # [1, 2, 3]
L[-4:-1:2] # [1, 3]
```

#### 字符串切片

> 可将字符串看成list

### 迭代

#### 介绍

> 通过 `for ... in` 完成迭代
> Python 的 for循环不仅可以用在list或tuple上，还可以作用在其他任何可迭代对象上。

#### 索引迭代

> Python中，迭代永远是取出元素本身，而非元素的索引。
> 对于有序集合，元素确实是有索引的。有的时候，我们确实想在 for 循环中拿到索引，此时使用 `enumerate() 函数`。

```
>>> L = ['Adam', 'Lisa', 'Bart', 'Paul']
>>> for index, name in enumerate(L):
...     print index, '-', name
... 
0 - Adam
1 - Lisa
2 - Bart
3 - Paul
```

> 实际 `enumerate()` 所做的是将['Adam', 'Lisa', 'Bart', 'Paul']变成了[(0, 'Adam'), (1, 'Lisa'), (2, 'Bart'), (3, 'Paul')]

#### 迭代dict

> dict 对象有一个 values() 方法，这个方法把dict转换成一个包含所有value的list
> dict除了values()方法外，还有一个 itervalues() 方法，用 itervalues() 方法替代 values() 方法，迭代效果完全一样
> values() 方法实际上把一个 dict 转换成了包含 value 的list。但是 itervalues() 方法不会转换，它会在迭代过程中依次从 dict 中取出 value，所以 itervalues() 方法比 values() 方法节省了生成 list 所需的内存。

```
d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }
print d.values()
# [85, 95, 59]
for v in d.values():
    print v
# 85
# 95
# 59

d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }
print d.itervalues()
# <dictionary-valueiterator object at 0x106adbb50>
for v in d.itervalues():
    print v
# 85
# 95
# 59
```

#### 迭代dict的key与value

> items() 方法把dict对象转换成了包含tuple的list，我们对这个list进行迭代，可以同时获得key和value
> 和 values() 有一个 itervalues() 类似， items() 也有一个对应的 iteritems()，iteritems() 不把dict转换成list，而是在迭代过程中不断给出 tuple，所以， iteritems() 不占用额外的内存。

```
for key, value in d.items():
     print key, ':', value      
# Lisa : 85
# Adam : 95
# Bart : 59
```

### 列表生成式

> 要生成 `[1*1, 2*2, 3*3, ... 100*100]` 的数据时，Python有一种特殊的列表生成式可以用简洁的代码生成list

```
[n * n for n in range(1, 101)] # [1, 4, 9, 16, ... 10000]
```

#### 条件过滤

> 添加if判断后只有满足条件的项才会加入list中

```
[n * n for n in range(1, 101) if n % 2 == 0] # [4, 16, 36, 64, ... 10000]
```

#### 多层表达式

> for循环可以嵌套，因此，在列表生成式中，也可以用多层 for 循环来生成列表。

```
[m + n for m in 'ABC' for n in '123'] # ['A1', 'A2', 'A3', 'B1', 'B2', 'B3', 'C1', 'C2', 'C3']
```