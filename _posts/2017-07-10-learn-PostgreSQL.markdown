---
title: 学习PostgreSQL
layout: post
category: SQL
tags: 数据库 学习
---

##### 安装之后允许non-host连接

**修改data目录下的`pg_hba.conf`**

`host all all 0.0.0.0/0 trust`

> all database all users all host will be trust

##### 常用的数据库命令

    # 控制台连接数据库
    psql -U user -d database -h host -p port

    # 

    # 控制台常用命令
    \h: 查看sql命令的解释,比如\h select
    \?: 查看sql的命令列表
    \l: 列出所有的数据库
    \c [database_name]: 连接其他数据库
    \d: 列出当前数据库的所有表格
    \d [table_name]: 列出一张表格的结构
    \du: 列出所有的用户
    \e: 打开文本编辑器
    \conninfo: 列出当前的数据库和连接信息
    \password user_name: 为用户设置密码
    \q: 退出控制台

##### 用户管理常用命令-控制台

    # 创建用户[设置密码]
    create user user_name [with passord 'password'];

    # 创建数据库并指定拥有者
    create database database_name owner user_name;

    # 将数据库(database_name)的所有权都赋予用户(user_name),否则用户只能登陆,没有任何数据库操作权限
    grant all privileges on database database_name to user_name

    # 创建超级用户
    create user user_name superuser password 'password';

    # 删除用户
    drop user if exists user_name 

    # 为用户指定查询路径(search_path)
    alter user user_name set search_path to schema_name, database_name;

##### 用户管理常用命令-shell

    # 创建用户
    sudo -u postgres createuser --superuser user_name

    # 设置密码
    \password user_name

    # shell命令下创建数据库并指定拥有者
    sudo -u postgres createdb -O user_name database_name

