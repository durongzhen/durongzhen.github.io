---
title: centos7常用命令
categories: 总结
date: 2020-04-04 16:24:27
tags: centos7命令
copyright: true 
---

> **一些Centos7常用命令，记录下来方便查找**


程序|启动|关闭|重启|状态
-|-|-|-|-
apache|```systemctl start httpd```|`systemctl stop httpd`|`systemctl restart httpd `|`systemctl status httpd `
mysql|`systemctl start mysqld `|`systemctl stop mysqld`|`systemctl restart mysqld`|`systemctl status mysqld`
php-fpm|`systemctl start php-fpm`|`systemctl stop php-fpm`|`systemctl restart php-fpm`|`systemctl status php-fpm`
nginx|`systemctl start nginx` 或 `service nginx start` 或 `./nginx`|`systemctl stop nginx` 或 `service nginx stop` 或 `./nginx -s stop`|`systemctl restart nginx` 或 `service nginx restart` 或 `./nginx -s reload`|`systemctl status nginx` 或 `service status nginx`

<!--more-->
---
作用|命令
-|-
查看端口| `netstat -lnp \| grep 端口号`
查程序| `ps -ef \| grep 程序名`
nginx判断配置文件|`./nginx -t`
设置开机启动(eg:Apache)|`systemctl enable httpd.service`
关闭开机启动(eg:Apache)|`systemctl disable httpd.service`
检查是否设置开机自启(eg:Apache)|`systemctl list-unit-files \| grep httpd` 
Linux系统版本| `lsb_release -a`
Linux内核版本| `cat /proc/version`
查看操作系统版本 | ` head -n 1 /etc/issue  `
查看CPU信息 | `cat /proc/cpuinfo  `
查看计算机名 |` hostname  `
查看环境变量资源 | `env `
查看内存使用量和交换区使用量 | ` free -m  `
查看各分区使用情况 | `df -h `
查看指定目录的大小 | ` du -sh 目录名  `
查看内存总量 | `grep MemTotal /proc/meminfo `
查看空闲内存量 | ` grep MemFree /proc/meminfo `
查看系统运行时间、用户数、负载 | ` uptime `
查看系统负载磁盘和分区 | `cat /proc/loadavg `
查看挂接的分区状态 | ` mount \| column -t `
查看所有分区 | ` fdisk -l  `
查看所有交换分区 | `swapon -s `
查看所有网络接口的属性 | ` ifconfig  `
查看路由表 |  `route -n ` 
查看所有监听端口 | ` netstat -lntp  `
查看所有已经建立的连接 | ` netstat -antp `
查看网络统计信息进程 | ` netstat -s  `
查看所有进程 | ` ps -ef  `
实时显示进程状态用户 | ` top  `
查看活动用户 | ` w  `
查看指定用户信息 | ` id 用户名 `
查看用户登录日志 | ` last  `
查看系统所有用户 | `cut -d: -f1 /etc/passwd `
查看系统所有组 | `cut -d: -f1 /etc/group `
列出所有系统服务 | ` chkconfig –list  `
列出所有启动的系统服务程序 | ` chkconfig –list \| grep on  `
查看所有安装的软件包 | ` rpm -qa `



---

安装PHP 7.0、7.1的yum源，然后再执行安装扩展。

php 7.0以及扩展:

``` bash
yum install php70w php70w-fpm php70w-cli php70w-common php70w-devel php70w-gd php70w-pdo php70w-mysql php70w-mbstring php70w-bcmath php70w-xml php70w-pecl-redis php70w-process php70w-intl php70w-xmlrpc php70w-soap php70w-ldap php70w-opcache
```

php 7.1以及扩展:
``` bash
yum install php71w php71w-fpm php71w-cli php71w-common php71w-devel php71w-gd php71w-pdo php71w-mysql php71w-mbstring php71w-bcmath php71w-xml php71w-pecl-redis php71w-process php71w-intl php71w-xmlrpc php71w-soap php71w-ldap php71w-opcache
```

php 7.2以及扩展:
```bash
yum install -y php72w php72w-fpm php72w-cli php72w-common php72w-devel php72w-gd php72w-pdo php72w-mysql php72w-mbstring php72w-bcmath php72w-xml php72w-pecl-redis php72w-process php72w-intl php72w-xmlrpc php72w-soap php72w-ldap php72w-opcache
```
---


