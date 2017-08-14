---
layout: post
title: Git基本语法 
categories: 笔记
tags: git
---

### Git Clone

`$ git clone url`

url可以写成两种情况

* url = https://github.com/FengMengZhao/FengMengZhao.github.io.git

* url = git@github.com:FengMengZhao/FengMengZhao.github.io.git

> FengMengZhao 为 github 的 username；FengMengZhao.github.io 为仓库(Repository)的名称

> 最好使用第二个URL，第一个URL每次在进行push的时候需要输入密码，如果需要可以使用`git remote set-url origin git@github.com:username/repo.git`

### Git Modification Status

`$ git status`

### Git update Modification to local 

`$ git add .`

### Git undate Modification to log(real update)

`$ git commit -m"Title"`

> Title 为修改的说明

### Set remote git push url

`$ git remote set-url origin url`

> url为原始的URL( https://github.com/ 或者 git@github.com: )

> To ingnore input username and password during push remote, we must use URL"git@github.com:"

> 例如：`https://fmzhao:FENG799520.Github@github.com/fmzhao/fmzhao.github.io.git`

### push local repository to remote

`$ git push origin master`

### Git update local repository to remote

`$ git pull origin master`

### Git ignore deleted file

`$ git checkout -- .`

### Github的SSH配置

* 设置Git的User name 和 Email

`$ git config --global user.name "xxx"`

`$ git config --global user.email "xxx@gmail.com"`

* 生存密匙

`$ ssh-keygen -t rsa -C "xxx@gmail.com"`

> 按三个回车键，密码为空，得到两个文件：id_rsa 和 id_rsa.pub

* 在自己的git设置中添加密匙ssh: ssh-add

> 添加的是id_rsa.pub文件夹里的内容, 将id_rsa_pub用文本编辑器打开，复制其中的内容到对应的地方，点击添加即可

> 如果原来的remote URL 是`https://github.com/USER_NAME/*.git`的形式, 要将remote URL重新设置为`get@github.com:USER_NAME/*.git`

***

***

第一次上传Github Repository

	git inint
	git add .
	git commmit -m"firstUpdate"
	git remote add origin https://github.com/FengMengZhao/StudentsManagerWeb.git
	git push -u origin master

> 本人git密码是 前面正规+核心域名小写

[More...](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

#### git 忽略掉删除的文件

     git add --a
     git commit -m" "
     git push origin master

**git恢复删除的文件**

`git checkout -- .`

**windows git status 中文乱码**

`git config --global core.quotepath false`

**git将用户名(username)和密码(passwd)加入remote url**

`git remote set-url origin https://username:passwd@github.com/repo.git`

例如:`git remote set-url origin https://fmzhao:FENG799520.Github@github.com/fmzhao/fmzhao.github.io.git`

> 这样clone一个项目之后(自己的账号,知道用户名和密码),直接可以push而不需要ssh设置

**git重命名文件**

`git mv old_filename new_filename`
