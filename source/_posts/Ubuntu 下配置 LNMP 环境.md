---
title: Ubuntu 下配置 LNMP 环境
date: 2017/08/01 14:45:30
tags: 
	- LNMP
categories: 
	- 编程
---

配置 LNMP 环境

<!-- more -->

### 更新仓库

```
$ sudo apt-get update
```

### 安装语言包

```
$ sudo apt-get install -y language-pack-en-base
```

### 设置语言

```
$ sudo locale-gen en_US.UTF-8
```

### 添加PPA安装PHP7.1（如果你的Ubuntu是 14.04 ）

```
$ sudo apt-get install software-properties-common
$ sudo LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php
$ sudo apt-get update
```

### 安装PHP7.1

```
$ sudo apt-get -y install php7.1
```

### 安装 Laravel 所需的模块

```
$ sudo apt-get -y install php7.1-curl php7.1-xml php7.1-mcrypt php7.1-json php7.1-gd php7.1-mbstring php7.1-mysql php7.1-fpm php7.1-zip
```

### 安装 Mysql

```
$ sudo apt-get install mysql-server-5.7
```

### 安装 Nginx

```
$ sudo apt-get install nginx
```