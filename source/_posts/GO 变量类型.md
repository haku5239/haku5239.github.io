---
title: GO 变量
date: 2021-03-23 15:33:02
tag: 
	- GO
---



#### 常量

`const`

#### 整型

`int`, `int8`, `int16`, `int32`, `int64`

#### 浮点型

`float32`, `float64`

#### 字符

`byte`

#### 字符串

`string`

#### 数组

`[n]int`, `[n]string` ... 等等各种变量类型的数组，n必须是一个确定的数字，表示数组的长度，但是在声明时直接定义值可是省略成`...`，由go自己判断长度，如果下：

```go
arr := [...]int{1, 2, 3}
```

#### 切片(slice)

```go
arr_str := new([]byte)
arr := [...]int{1, 2, 3, 4, 5, 6}
arrSlice := arr[2:3:5]
fmt.Println(arr_slice, cap(arrSlice)) // [3] 3 
```

#### 字典(map)

```go
// 方式1
var numbers map[string]int
// 方式2
numbers := make(map[string]int)
// 声明并赋值
numbers := map[string]int{"one": 1, "two": 2}
```

#### 零值

##### 关于 “零值”，所指并非是空值，而是一种 “变量未填充前” 的默认值，通常为 0。

```go
int     0
int8    0
int32   0
int64   0
uint    0x0
rune    0 // rune 的实际类型是 int32
byte    0x0 // byte 的实际类型是 uint8
float32 0 // 长度为 4 byte
float64 0 // 长度为 8 byte
bool    false
string  ""
```

