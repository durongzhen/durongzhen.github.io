---
title: linux使用nohup执行jar
categories: 教程
date: 2020-04-04 16:35:24
tags: nohup
copyright: true 
---
```bash
java -jar XXX.jar &
```
- 命令结尾没有 "&"，则变成 "java -jar XXX.jar，表示在当前ssh窗口，可按CTRL + C打断程序运行，或者直接关闭窗口，则程序直接退出。
- 命令结尾添加 "&" ，则变成 “java -jar XXX.jar &”，表示在当窗口关闭时，程序才会中止运行。&代表让该命令在后台执行。


```bash
nohup java -jar XXX.jar > Log.log & 
或者
nohup java -jar XXX.jar >> Log.log &
```
- 命令 "nohup java -jar XXX.jar &" 部分，表示不挂断运行命令,当账户退出或终端关闭时,程序仍然运行。注意，该作业的所有输出被重定向到nohup.out的文件中。
- 命令 "nohup java -jar XXX.jar > Log.log &" 部分，表示不挂断运行命令,当账户退出或终端关闭时,程序仍然运行，并且该作业的所有输出被重定向到Log.log的文件中。“ > Log.log ” 该命令就是指定日志输出的文件。
- ">>"表示将输出以追加的方式重定向到Log.log中。

<!--more-->

```bash
nohup java -jar XXX.jar > Log.log 2>&1 & 
或者
nohup java -jar XXX.jar >> Log.log 2>&1 & 
或者
nohup java -jar XXX.jar > /dev/null 2>&1 &
```
- 标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据。
- 标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据。
- 标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息。
- 屏蔽输出，起到禁止输出作用：/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到"禁止输出"的效果。
- “> Log.log 2>&1” ：表示将 stdout 和 stderr 合并后重定向到 Log.log