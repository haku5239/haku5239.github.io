---
title: Google Cloud Platform
date: 2017/08/01 14:07:02
tags: 
	- Google
categories: 
	- 编程
---

## 终端连接服务器

```
$ ssh -i ~/.ssh/my-ssh-key [USERNAME]@[EXTERNAL_IP_ADDRESS]
```

使用原来的命令去链接谷歌服务器，可以看到命令很长，而且还要记 **IP** ，就算不记 **IP** 每次要复制也很麻烦，下面介绍一个小方法，输入简单的自定义命令就可以链接谷歌服务器。

<!-- more -->

### 生成公钥和私钥

文件保存在 .ssh 目录下名为 my-ssh-key  用户名[USERNAME]

```
$ ssh-keygen -t rsa -f ~/.ssh/my-ssh-key -C [USERNAME]
```

设置私钥为只读

```
$ chmod 400 ~/.ssh/my-ssh-key
```

查看 my-ssh-key.pub

```
$ cat ~/.ssh/my-ssh-key.pub
```

将公钥保存到谷歌云元数据下的SSH密钥下

### 快速连接

修改 .ssh 下的 config 文件 具体配置如下

```
$ vim ~/.ssh/config
Host gcloud
Hostname <IP>
Port 22
User <username>
IdentityFile ~/.ssh/google_compute_engine
```

使用 ssh gcloud 命令连接谷歌服务器

