---
title: 安装vlmcsd搭建KMS服务器
categories: 教程
date: 2020-04-04 16:30:26
tags: vlmcsd
copyright: true 
---
> vlmcsd搭建的KMS激活服务器，可以激活Windows和office（VL版）
微软原版镜像下载地址：[https://msdn.itellyou.cn/](https://msdn.itellyou.cn/ "https://msdn.itellyou.cn/")

### 搭建步骤：

- 下载vlmcsd文件：
```bash 
wget https://github.com/Wind4/vlmcsd/releases/download/svn1112/binaries.tar.gz
```
- 解压：
```bash
tar -xzvf binaries.tar.gz
```
- 进入目录：
```bash
cd binaries/Linux/intel/static
```
- 64位系统执行：
```bash
./vlmcsd-x64-musl-static
```
- 查看vlmcsd运行状态：
```bash
ps -ef | grep vlmcsd-x64-musl-static
```
<!--more-->

***注意：vlmcsd需要用到1688端口，如果你的机器防火墙打开了，需要设置放行规则或者关闭防火墙。***

### 使用步骤：

在需要激活的电脑上以管理员运行cmd，输入以下指令。

#### Windows激活步骤：
1. 
```bash
slmgr /skms 这里填写你的VPS公网IP或是解析到此IP的域名
```
2. 
```bash
slmgr /ato
```
3.
```bash
slmgr /xpr
```
重启即可激活。

#### Office激活步骤：

- 找到你的office安装目录，比如C:\Program Files (x86)\Microsoft Office\Office16

	该目录下面应该有个OSPP.VBS，接下来我们就cd到这个目录下面。

    ```bash
    cd C:\Program Files (x86)\Microsoft Office\Office16
    ```
- 执行注册kms服务器地址：

    ```bash
    cscript ospp.vbs /sethst:这里填写你的VPS公网IP或是解析到此IP的域名
    ```
- 一般来说，“一句命令已经完成了”，但一般office不会马上连接kms服务器进行激活，所以我们额外补充一条手动激活命令：

    ```bash
    cscript ospp.vbs /act
    ```
	如果提示看到successful的字样，那么就是激活成功了，重新打开office就好。

### 注意：你的Windows/OFFICE一定要是VL版本才能被激活！

