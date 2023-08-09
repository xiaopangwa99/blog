---
title: vscode远程免密连接
categories: 实用技巧
---
# 1.先在本地端生成密钥

## 生成SSH密钥

```bash
# -t 加密类型 -b 指定指定要创建的密钥的位数
$ ssh-keygen -t rsa -b 4096
```

连续按回车

## 查看公钥

```bash
$ cat ~/.ssh/id_rsa.pub
```

将``id_rsa.pub``中的内容复制下来

# 2.将本地端公钥添加至远程端

## 添加

```bash
$ cd ~/.ssh
$ vim authorized_keys #
```

将从``id_rsa.pub``中复制的内容贴进``authorized_keys``中

## 权限设置

```bash
$ chmod 600 authorized_keys  #所有者可读写
```

# 3.vscode端

## ssh config

```bash
Host $远程主机名$   #可以自定义，目的是知道自己用什么主机
  HostName $远程主机IP$
  User $用户名$
  Port $ssh端口$   #不写默认22
  IdentityFile $本机SSH私钥路径$
  ForwardAgent yes $希望使用本地电脑里的密钥登录，且不想把这个密钥发送到堡垒机，之前添加 -A生成$
```

一般只配置``Host`` |``HostName``|``User``即可
