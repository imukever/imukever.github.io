---
title: "Gitlab代码托管和自动化CI"
layout: post
date: 2016-09-01 10:45：00
tag:
- ubuntu
- Gitlab
- CI
blog: true
author: Mukever
---

***Gitlab的安装***

使用清华源配置Gitlab
```
https://mirror.tuna.tsinghua.edu.cn/help/gitlab-ce/
```
  ![Alt text](../png/gitlab-tuna.png)

因为gitlab需要配置邮件提醒，所以需要提前配置163邮箱的stmp

  ![Alt text](../png/stmp.png)


修改配置文件

```
sudo vim /etc/gitlab/gitlab.rb
```
修改的具体内容如下

  ![Alt text](../png/gitlab.png)

  gitlab['smtp_password']为自己设置的stmp密码（不是163邮箱的密码）

  ![Alt text](../png/gitlab-mail.png)

注意：user['git_user_email'] 要和gitlab['smtp_user_name']一致

  ![Alt text](../png/gitlab-mail-user.png)

配置完成之后，启动gitlab

```
sudo gitlab-ctl configure
```
配置成功后出现的界面（至于logo部分，可以自行修改）

  ![Alt text](../png/gitlab-login.png)

***配置CI***

同样使用清华的源，先安装docker，安装时如果出错，请停止gitlab。如果没有错误提示，按照清华源提示操作。

```
sudo gitlab-ctl stop
```

  ![Alt text](../png/docker.png)

同样使用清华的源，安装gitlab-ci-multi-runner

  ![Alt text](../png/ci.png)

新建一个项目，推到gitlab

然后配置 .gitlab-ci.yml

  ![Alt text](../png/ci-test.png)

注册runner

记住url和token
  ![Alt text](../png/runner.png)

  ```
  sudo gitlab-runner register
  ```
  ![Alt text](../png/register.png)

开启gitlab-runner

    ```
    sudo gitlab-runner run
    ```


成功的结果
  ![Alt text](../png/success.png)


gitlab-ci配置文件教程
```
http://docs.gitlab.com/ce/ci/yaml/README.html#cache
```
