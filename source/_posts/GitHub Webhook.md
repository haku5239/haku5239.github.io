---
title: GitHub Webhook
date: 2017/7/20 15:22:39
tags: 
	- GitHub
categories: 
	- 编程
---

托管于 [GitHub](https://github.com) 的项目，当一个功能在本地写完调试完没有问题之后，想要提交上去更新到服务器，测试一下是否有问题，当本地提交到 GitHub 后却还要去服务器更新一下，其实有时候感觉还是小麻烦的~

<!-- more -->

### 部署公钥

移动到当前用户目录下，创建公钥和私钥（当然此处只用到公钥）

```
$ cd
$ sudo ssh-keygen -t rsa -C "your_github_email"
```

公钥在 `/home/aixieluo/.ssh` 目录下，此处的 aixieluo 是我的用户名称，登录 [GitHub](https://github.com) ，进入 `Settings` => `SSH and GPG keys` => `New SSH key` ，Title 自定义输入，Key 则是 `/home/aixieluo/.ssh/ide_rsa.pub` 的内容

### 给 www-data 分配目录权限，部署公钥

```
$ sudo mkdir /var/www/.ssh
$ sudo chown -R www-data:www-data /var/www
$ cd /var/www
$ sudo -Hu www-data ssh-keygen -t rsa 
```

生成的公钥在 `/var/www/.ssh` 目录下，登录 [GitHub](https://github.com) ，进入需要同步的项目的主页，进入 `Settings` => `Deploy keys` => `Add deploy key` ，Title 自定义输入，Key 则是 `/var/www/.ssh/ide_rsa.pub` 的内容

### clone 项目

这部是最为关键的，必须使用 www-data 用户 clone 项目，这样自动更新项目时会默认使用 www-data 用户

```
$ cd /var/www 
$ sudo -Hu www-data git clone git@github.com:aixieluo/study.git
```

### 配置钩子

依旧是登录 [GitHub](https://github.com) ，进入需要同步的项目的主页，进入 `Settings` => `WebHooks` => `Add webhook` ，以下是我的配置：

![webhook](../img/webhooks/img1.png)

此处例子项目是 Laravel5.4 ，配置过程如下

> **api.php** 文件的配置： `Route::post('deploy', 'DeploymentController@deploy');`
> **VerifyCsrfToken.php** 文件的配置： `protected $except = ['api/deploy'];` ，此处为了排除 **csrf** 验证
> **deploy** 方法实现如下：
>	```
    public function deploy(Request $request) {
        $commands = ['cd /var/www/study', 'git pull'];
        $signature = $request->header('X-Hub-Signature');
        $payload = file_get_contents('php://input');
        if ($this->isFormGitHub($payload, $signature)) {
            foreach ($commands as $command) {
                shell_exec($command);
            }
            http_response_code(200);
        } else {
            abort(403);
        }
    }

    public function isFormGitHub($payload, $signature) {
        return 'sha1=' . hash_hmac('sha1', $payload, env('GITHUB_DEPLOY_TOKEN'), false) === $signature;
    }
    ```
> 此处的 `GITHUB_DEPLOY_TOKEN` 就是在 GitHub 的 webhook 里配置的 Secret