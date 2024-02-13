---
title: CentOS安装MySQL
categories: 实用技巧
tags: 
    - MySQL
date: 2024-02-11 15:00:00
description: 避坑小指南
cover: https://yym-tuchuang.oss-cn-hangzhou.aliyuncs.com/blog/2024-02-11/%20cover.jpeg
top_img: rgba(0,0,0,0)
---
# centos安装MySQL

因为经常使用包管理器安装软件，故用``yum install mysql``的方法进行安装。安装完毕后发现各种各样的问题，所以重新进行安装。

# 1.卸载MariaDB

查看是否安装有MariaDB

```bash
rpm -qa | grep mariadbs
```

![](https://yym-tuchuang.oss-cn-hangzhou.aliyuncs.com/blog/2024-02-11/%201.png)

若存在，则卸载

```bash
rpm -e --nodeps mariadb-libs
```

卸载后重复执行上述命令，若未出现上图内容则卸载成功

# 2.安装MySQL

[MySQL社区版下载]([MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/))

这里使用wget下载

```bash
wget https://dev.mysql.com/get/mysql80-community-release-el7-11.noarch.rpm
```

在下载好的目录下进行安装

![](https://yym-tuchuang.oss-cn-hangzhou.aliyuncs.com/blog/2024-02-11/%202.jpeg)

```bash
rpm -ivh mysql80-community-release-el7-11.noarch.rpm
```

```bash
yum install mysql-community-server.x86_64
```

# 3.开启服务

```bash
cd /var/lib/mysql
```

该目录下此时应该是空的

![](https://yym-tuchuang.oss-cn-hangzhou.aliyuncs.com/blog/2024-02-11/%203.jpeg)

启动MySQL服务

```bash
systemctl start mysqld
```

此时目录下就有文件了，MySQL初始化完成

![](https://yym-tuchuang.oss-cn-hangzhou.aliyuncs.com/blog/2024-02-11/%204.jpeg)

# 4.修改默认密码

查看默认密码

```bash
grep 'password' /var/log/mysqld.log
```

![](https://yym-tuchuang.oss-cn-hangzhou.aliyuncs.com/blog/2024-02-11/%205.jpeg)

冒号后面的内容即为默认密码

```bash
mysql -u root -p[默认密码]
```

修改密码可以用以下sql语句

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '新密码'
```

看到``Query OK``的提示，即为修改成功。

至此结束