---
layout: post
title: "swoole exception"
date: 2019-01-22
description: "swoole exception解决"
tag: Swoole
---

swoole启动一段时间后报以下错误
```
[2018-11-06 11:48:14 #3236564.8]        ERROR   swServer_master_onAccept (ERROR 502): accept() failed. Error: Too many open files[24]
[2018-11-06 11:48:15 #3236564.8]        ERROR   swServer_master_onAccept (ERROR 502): accept() failed. Error: Too many open files[24]
[2018-11-06 11:48:16 #3236564.8]        ERROR   swServer_master_onAccept (ERROR 502): accept() failed. Error: Too many open files[24]
```
需要修改`ulimit -n`

```
#!/bin/bash

initSys(){
    # 初始化整个系统
    echo -e '* soft nofile 65536 \n * hard nofile 65536 \n * soft nproc 65536 \n * hard nproc 65536' > /etc/security/limits.d/d3-limits.conf
    # 开始配置/etc/teryx.conf的信息
    echo -e 'net.ipv4.tcp_fin_timeout=30\nnet.ipv4.tcp_syncookies=1\nnet.ipv4.tcp_tw_recycle=1\nnet.ipv4.tcp_tw_reuse=1 \n' > /etc/sysctl.d/teryx.conf
}

fInstall()
{
    initSys

    sysctl -p
    sysctl -p /etc/sysctl.d/teryx.conf
}

fInstall $@

```
