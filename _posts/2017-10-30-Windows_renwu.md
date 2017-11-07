---
layout: post
title: "Windows定时任务"
date: 2017-10-30
description: "Windows定时任务"
tag: Windows

---
### 1.准备需要执行的文件（PHP文件为例）
```
<?php 
$mysqli = new mysqli('127.0.0.1', 'root', '','test');
$query = "INSERT INTO `bk_zan` VALUES ('10', '1', '2', '3')";
if ($mysqli->connect_error) {
 	die('Connect Error (' . $mysqli->connect_errno . ') '
            . $mysqli->connect_error);
} else {
	echo 'ok';
	mysqli_query ($mysqli,$query);
}
$mysqli->close();
```
如若要持续PHP文件就需要安装PHP程序，如果PHP文件连接数据库的话同样需要安装好数据库环境
### 2.创建定时任务文件cron.bat(文件后缀为.bat)
```
E:\wamp64\bin\php\php7.0.10\php.exe -q C:\Users\abc\Desktop\autocheck.php
```
前面为用来执行文件的程序 后面为需要执行的文件
### 3.在Windows上添加定时任务
打开windows10的控制面板->大图标显示->管理工具->任务计划程序->操作->创建任务
![](/images/posts/Windows/kongzhimianban.jpg)
![](/images/posts/Windows/renwujihua.jpg)
![](/images/posts/Windows/tianjiarenwu.jpg)
![](/images/posts/Windows/tianjiamignzi.jpg)
![](/images/posts/Windows/tianjiashijian1.jpg)
![](/images/posts/Windows/tianjiashijian2.jpg)
![](/images/posts/Windows/tianjiacaozuo1.jpg)
![](/images/posts/Windows/tianjiacaozuo2.jpg)
### 点击确认所有操作完成之后，在任务列表里可以查看到刚刚自定义的定时任务,到了指定的时间指定的程序就会被运行
![](/images/posts/Windows/renwuliebiao.jpg)
### 注意：
1. 电脑不能自动睡眠 自动睡眠之后自动任务是不会执行的
2. 查看自动任务的触发器是否开启
3. 其中还有其他的更多自定义操作设置可以自行摸索