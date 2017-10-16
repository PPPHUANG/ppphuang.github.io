---
layout: post
title: "使用ssh连接ubantu"
date: 2017-08-30
description: "使用ssh连接ubantu"
tag: ubantu

---

### 1.ubantu安装ssh服务

`sudo apt-get install openssh-server`

`ps -e | grep ssh`

查看`sshserver`是否启动 如果只有`ssh-agent`那`ssh_server`还没有启动,需要`/etc/init.d/ssh start`，如果看到`sshd`那说明`ssh-server`已经启动了。

### 2.将虚拟机的网络模式调整为桥接模式

在虚拟机的网络设置里设置为桥接模式

### 3.修改ubantu中的interfaces文件

`sudo vim /etc/network//interfaces`

如果提示未安装`vim`

`sudo apt install vim`

修改如下

```
auto eth0
iface eth0 inet static
address 192.168.1.251
netmask 255.255.255.0
gateway 192.168.1.1
```

需要网段相同，以上以物理机地址192.168.1.133为例

### 4.查看物理机的IP

`ipconfig`

### 5.查看ubantu IP

`ifconfig`

如果提示未安装`net-tools `

`sudo apt install net-tools `

### 6.xshell或者putty连接

使用查看到的ubantu IP连接ubantu,需要ubantu的账号密码
