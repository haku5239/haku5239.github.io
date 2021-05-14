---
title: 解决gitignore不生效问题
date: 2017/09/05 15:45:45
tags: 
	- Git
	- reason
categories: 
	- Git
---

关于在项目开发过程中，将某些文件或者文件夹加入到 `.gitignore` 但是却并没有生效的问题，原因是因为 `.gitignore` 只能忽略那些原来没有被 `track` 的文件，如果这些文件已经被纳入了版本管理中，则修改 `.gitignore` 是无效的。解决办法就是先将本地缓存删除（改变成为 `track` 的状态），然后再提交

> git rm [-r] --cached 不生效的文件或者目录（目录时需要加-r
> git add .

