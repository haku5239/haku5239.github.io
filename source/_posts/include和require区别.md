---
title: include和require区别
date: 2021/05/14 14:05:47
tags:
    - blog
categories:
    - 编程
---


### include和require区别 

- 引入的方式不同

  > `include`会读取文件，并执行内部的程序
  >
  > `require`会引入文件内的内容，代替自身

- 当文件不存在时，处理行为不同

  > `include`会产生一个警告，但是脚本会继续执行
  >
  > `require`会产生一个致命错误，并停止运行

