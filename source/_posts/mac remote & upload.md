---
title: MacOS远程连接服务器及文件传输
categories: 实用技巧
tags: 
    - MySQL
    - SSH
date: 2024-02-25 15:00:00
description: 利用原生zsh实现，不需借助其他工具
cover: https://yym-tuchuang.oss-cn-hangzhou.aliyuncs.com/blog/2024-02-25/top.jpeg
top_img: rgba(0,0,0,0)
---
# mac远程连接服务器

## 1.通过ssh直接连接

```bash
ssh username@hostname [-p 端口号]
```

使用默认SSH端口（22）则可省略-p参数

每次登陆都需要输入``username``、``hostname``、``password``，比较麻烦

## 2. ssh key认证

### 2.1生成ssh密钥

```sh
ssh-keygen -t rsa -C "your_email@example.com"
```

生成后在``.ssh``目录下会生成私钥``id_rsa``和公钥``id_rsa.pub``

### 2.2配置

将公钥``id_rsa.pub``中内容复制到服务器中``~/.ssh``目录下``authorized_keys``文件中

在``~/.ssh``下新建config文件

```bash
vim ./ssh/config
```

编辑config文件

```bash
Host 123											//别名
	hostname xx.xx.xx.xx				//ip
	username xx									//用户名
	IdentityFile ~/.ssh/id_rsa 	//认证私钥
```

这时打开终端可以直接利用别名免密连接服务器

```bash
ssh 123
```

### 2.3断连问题

mac终端连接服务器长时间不操作会出现断连问题，在网上查阅资料后给出以下解决方案

在config文件中进行配置

如果是想让主机所有用户都生效修改``/etc/ssh/ssh_config``

如果只让本用户生效，则修改``~/.ssh/config``

```bash
Host *
	ServerAliveInterval 30   //server每隔60秒发送一次请求给client，client相应，从而保持连接
	ServerAliveCountMax 3		
```



## 2.文件传输

mac上实现文件传输可通过``scp``命令

上传文件

```bash
scp /path/filename username@hostname:/path/file
```

下载文件

```bash
scp username@hostname:/path/file （本机）/path/file
```

上传、下载目录

```bash
scp -r #同上，文件修改为目录即可
```



​                                                                                                                                                                                              