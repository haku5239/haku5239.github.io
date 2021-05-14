---
title: git pull request
date: 2017/7/25 12:22:39
tags: 
	- GitHub
categories: 
	- GitHub
---

创建一个 `pull request` 的步骤如下：

<!-- more -->

1. `fork` 想要贡献代码的项目A

2. 使用 `git clone <address>` 从自己的 [GitHub](https://github.com) 载下 `fork` 回来的项目

3. 进入项目目录

4. 使用 `git remote add <origin name> <address>` 添加远程分支，此处的 `address` 为项目A的 GitHub 地址，推荐将 `origin name` 命名为 `upstream`

5. 此时先使用 `git pull <origin name> master` 检查原作者是否有新的更新

6. 创建分支 `git checkout -b <branch>`

7. 编写你想要贡献的功能代码

8. 写完代码后进行 `git commit`

9. 切换到 `master` 分支，再次使用 `git pull <origin name> master` 检查原作者是否有新的更新，获取最新代码后切换回后来创建的分支 `<branch>`

10. 测试后没有问题后使用 `git rebase master` 同步 `commit` 历史记录

11. 最后使用 `git push origin <branch>` 提交到远程仓库

12. 登录到 [GitHub](https://github.com) ，使用 `compare & pull request` 或者 `new pull requset` 按钮，创建一个 `pull request` ，等原作者 `merge` 你的 `pull request` 时，你就成功的为这个项目贡献了代码