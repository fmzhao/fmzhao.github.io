---
layout: post
title: 学习MySQL
category: SQL 
tags: MySQL 数据库 学习
---

##### 用户管理命令

    # 创建新的用户和密码
    CREATE USER user_name [IDENTIFIED BY 'password']

    # 赋予用户权限
    GRANT ALL PRIVILEGES ON *.* TO user_name@host_name IDENTIFIED BY 'password'

    # 查看所有的用户
    SELECT host, user, password from mysql.user;

