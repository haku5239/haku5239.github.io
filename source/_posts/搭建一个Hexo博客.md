---
title: 搭建一个Hexo博客
date: 2017/6/13 20:46:25
tags: 
	- Hexo
	- DropBox
categories: 
	- 开发环境
---

### 概述

在朋友的推荐下，尝试了使用 Hexo + DropBox 搭建博客
本文中环境为 Ubuntu16.04 LTS 64bit。

<!-- more -->

### 优点

Hexo:

* Hexo 快速、简洁且高效
* 使用 Markdown 解析文章，书写方便
* 配有较为详细的中文官方文档，适于新人上手
* 安装简单
* 主题库丰富，新手刚上手不需要了解太多即可配置出靓丽的博客网站

DropBox:

* 提供的免费空间足以自用存储文章
* 各平台自动同步刷新资源

### 参考文档

[使用Dropbox+Justwriting+Markdown搭建个人博客](http://php-justwriting.rhcloud.com/post/dropbox-justwriting-markdown)
[Hexo 官方文档](https://hexo.io/zh-cn/api/index.html)

### 安装 Dropbox Client

32位系统

```
$ cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86" | tar xzf -
```

64位系统

```
$ cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
```

启动 DropBox12

```
$ ~/.dropbox-dist/dropboxd
```

如果你是第一次在你的服务器运行 DropBox，复制提示的链接在浏览器中打开，用你的DropBox用户登录即可完成对服务器的授权。授权后，手动 Control + C 终端这个脚本。

```
$ wget https://www.dropbox.com/download?dl=packages/dropbox.py -O dropbox.py
$ python dropbox.py start
```

修改 DropBox 目录权限

```
$ sudo chmod 775 ~/Dropbox/
```

至此，DropBox 配置完成。

### 安装 Hexo

安装 Hexo 非常简单，然而安装之前你的电脑里已经安装了以下应用程序：

[Git](https://git-scm.com)
[Node.js](http://nodejs.org)

安装 Git ：

```
$ sudo apt install git -y
```

安装 Node.js ：
推荐使用 nvm 安装，更易于版本管理

wget：

```
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
```

安装完成后，重启终端并执行下列命令即可安装 Node.js。

```
$ nvm install stable
```

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

```
$ npm install -g hexo-cli
```

### 建站

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

详细配置请直接查阅 [Hexo 配置](https://hexo.io/zh-cn/docs/configuration.html)

### 将之前的 DropBox 目录链接到 hexo 项目中

```
$ cd <你的项目名>/source/
$ rm -fr _posts
$ ln -s ~/Dropbox/ _posts
```

### 配置完成

以下命令，生成静态文件并部署网站

```
$ hexo g -d
```

以下命令，实现后台挂载 hexo 监听文件变动，自动生成静态文件并部署网站

```
$ nohup hexo g -d -w &
```



