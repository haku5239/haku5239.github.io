---
title: 搭建Apache+PHP+Mysql环境
date: 2017/6/13 20:46:25
tags: 
	- Apache
	- PHP
	- Mysql
	- Composer
categories: 
	- 开发环境
---

### 概述

本文开发环境为 Laravel 配置
本文中环境为 Ubuntu16.04 LTS 64bit。

<!-- more -->

### 安装 Apache2.4

```
$ sudo apt install apache2 -y
```

打开 Rewrite 模块

```
$ sudo a2enmod rewrite
```

修改 AllowOverride

```
$ sudo vim /etc/apache2/apache2.conf
```

允许在某目录下(如 `/var/www/` )使用“.htaccess”文件

```
<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>
```

新建站点

```
$ sudo vim /etc/apache2/sites-available/000-default.conf
```

修改站点信息

```
ServerName 你的网站地址
DocumentRoot 你的系统本地路径
```

### 安装 PHP7.0

```
$ sudo apt install php7.0 -y
```

配置 Apache 解析 PHP

```
$ sudo apt install libapache2-mod-php7.0 -y
```

安装常用扩展

```
$ sudo apt install php7.0-gd php7.0-mbstring php7.0-dom php7.0-mysql -y
```

### 安装 Composer

下载并安装 Composer

```
$ sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
$ sudo php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
$ sudo php composer-setup.php
$ sudo php -r "unlink('composer-setup.php');"
```

将 Composer 移动至全局环境

```
$ sudo mv composer.phar /usr/local/bin/composer
```

### 安装 Mysql5.7

[Mysql官方文档安装示例](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#apt-repo-fresh-install)

```
$ sudo apt-get install mysql-server -y
```

### 配置完成

重启 Apache2

```
$ sudo service apache2 restart
```

