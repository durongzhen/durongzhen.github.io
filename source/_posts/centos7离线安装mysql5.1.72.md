---
title: centos7离线安装mysql5.1.72
categories: 教程
date: 2020-04-04 14:53:18
tags:  mysql
copyright: true 
---

> 本文主要记录centos7离线安装mysql-5.1.72，用于没有联网环境下部署使用。

**安装前请先卸载centos7自带的Mariadb。**
- 查询命令 rpm -qa | grep mariadb
- 卸载命令 rpm -e --nodeps 文件名

1. 使用xshell连接服务器，将mysql-5.1.72-linux-x86_64-glibc23.tar.gz 源程序拷贝到目录 /usr/local 并解压。
```bash
tar –xzvf mysql-5.1.72-linux-x86_64-glibc23.tar.gz
```
2. 建立源软件目录与mysql目录软连接(/usr/local目录下操作)
```bash
ln -s mysql-5.1.72-linux-x86_64-glibc23 mysql
```
3. 建立系统目录/usr/bin与mysql目录软连接
```bash
ln -s /usr/local/mysql/bin/mysql /usr/bin
```
4. 添加一个系统用户，不创建目录，不允许用户登录。只是用户运行 mysql这个进程使用。
```bash
useradd -r -s /sbin/nologin mysql 
id mysql (查询是否建立成功)
```

<!--more-->

5. 配置my.cnf
```bash
cd /usr/local/mysql
cp support-files/my-medium.cnf /etc/my.cnf
vi /etc/my.cnf
```
在[mysqld]部分末尾添加`basedir = /usr/local/mysql `以及 `datadir = /usr/local/mysql/data`

6. 修改mysql文件夹权限为mysql
```bash
chown -R mysql:mysql /usr/local/mysql
```
7. 安装、初始化数据库
```bash
./scripts/mysql_install_db --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
```
8. 复制启动脚本到资源目录
```bash
cp ./support-files/mysql.server /etc/rc.d/init.d/mysqld
```
9. 增加mysqld服务控制脚本执行权限
```bash
chmod +x /etc/rc.d/init.d/mysqld
```
10. 将mysqld服务加入到系统服务
```bash
chkconfig --add mysqld
```
11. 检查mysqld服务是否已经生效
```bash
chkconfig --list mysqld
```
12. 启动mysql
```bash
service mysqld start
```
13. mysql权限收回给root(可选)
```bash
chown -R root:root /usr/local/mysql
```
