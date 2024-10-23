+++
title = 'Git'
date = 2024-10-23T17:32:25+08:00
draft = false
tags = [ 'git' ]
categories = '开发工具'
+++

## 忽略文件权限

```shell
git config core.filemode false
```


## 保存用户名和密码

先用 git 拉一次东西，拉的时候会提醒你输入帐号的密码

输入正确的帐号和密码后，等东西拉完以后输入

```shell
git config --global credential.helper store
```

以后就不用输入帐号和密码了

## 放弃本地更改

```shell
git fetch --all
git reset --hard origin/master 
git pull
```

## 全局安全目录

```shell
git config --global --add safe.directory "*"
```

## 常用命令

![git](/images/git.png)
