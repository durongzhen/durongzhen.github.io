---
title: Centos7在线安装MySQL5.7
categories: 教程
date: 2020-04-04 16:27:51
tags: mysql5.7
copyright: true 
---
### 一、 下载并安装MySQL官方的 Yum Repository

	`wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm`

- 使用上面的命令就直接下载了安装用的Yum Repository，大概25KB的样子，然后就可以直接yum安装了

	`yum -y install mysql57-community-release-el7-10.noarch.rpm`

- 开始安装MySQL服务器：

	`yum -y install mysql-community-server`

这步可能会花些时间，安装完成后就会覆盖掉之前的mariadb。

<!--more-->

### 二、MySQL数据库设置

- 启动mysql：

	`systemctl start  mysqld.service`

- 查看运行状态：

	`systemctl status mysqld.service`

- 此时MySQL已经开始正常运行，不过要想进入MySQL还得先找出此时root用户的密码，通过如下命令可以在日志文件中找出密码：

	`grep "password" /var/log/mysqld.log`

- 进入数据库：

	`mysql -uroot -p`

- 输入初始密码，此时不能做任何事情，因为MySQL默认必须修改密码之后才能操作数据库。另外mysql密码有一定规则，我们可以修改参数设置简单规则：

	`mysql> set global validate_password_policy=0;`

	`mysql> set global validate_password_length=1;`

- 设置之后此时密码就可以设置的很简单，例如123456之类的。到此数据库的密码设置就完成了。

	`ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';`

- 最后卸载Yum Repository，因为以后每次yum操作都会自动更新。使用如下命令：

	`yum -y remove mysql57-community-release-el7-10.noarch `