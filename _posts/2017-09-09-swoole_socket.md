---
layout: post
title: "初识Socket"
date: 2017-09-09
description: "初识Socke"
tag: Swoole

---

> 上次公司技术分享会，总监问我们有没有人知道`套接字`，尴尬的是我连听都没有听过，后来才知道Socket就是俗称的`套接字`。。。

### 什么是socket

Socket俗称`套接字`，用于描述IP地址跟端口，是一个通信链`句柄`。经常有人说Socket是比tcp/ip协议更高一层的一种协议。其实Socket既不是应用`程序`，也不是一种`协议`。是操作系统提供的通信层的一组抽象API，作用于tcp/ip协议之上（基于tcp/ip协议）。

### 使用Swoole制作web简易群聊

其实PHP中有内置Socket的操作函数库，但是较为麻烦，所以很少有人用。Swoole扩展发布之后，其中的Socket操作即为简便，所以使用Swoole扩展制作web简易群聊。

1. 服务器安装PHP，Swoole扩展（Swoole扩展不支持Windows，建议Linux）。不会安装查看博客目录中的ubantu16安装swoole
2. 编写服务端脚本server.php

```
<?php
$ws = new swoole_websocket_server("0.0.0.0", 9502);  //创建Swoole_sebsocket_server服务
$ws->user_fd = [];   //给ws对象添加属性user_fd，值为空数组,存放连接用户FD（文件描述符，类似用户id）；
//监听WebSocket连接打开事件
$ws->on('open', function ($ws, $request) {
        //将连接用户的FD存入到user_fd数组中
        $ws->user_fd[] = $request->fd;
    });
//监听WebSocket消息事件
$ws->on('message', function ($ws, $frame) {
        //拼接要群发消息的字符串
        $msg =  'from'.$frame->fd.":{$frame->data}\n";
        //将要群发的消息字符串循环发送到每一个连接的用户
        foreach($ws->user_fd as $v){
            $ws->push($v,$msg);
        }
    });
//监听WebSocket连接关闭事件
$ws->on('close', function ($ws, $fd) {
        //删除已断开的客户端
        unset($ws->user_fd[$fd-1]);
    });
//开启服务
$ws->start();
```

3. 编写客户端脚本wechat.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="msg"></div>
<input type="text" id="text">
<input type="submit" value="发送数据" onclick="song()">
</body>
<script>
    var msg = document.getElementById("msg");
    var wsServer = 'ws://192.168.5.143:9502';
    //调用websocket对象建立连接：
    //参数：ws/wss(加密)：//ip:port （服务端IP，创建的socket端口号）
    var websocket = new WebSocket(wsServer);
    //onopen监听连接打开
    websocket.onopen = function (evt) {
        msg.innerHTML = websocket.readyState;
    };

    function song(){
        var text = document.getElementById('text').value;
        document.getElementById('text').value = '';
        //向服务器发送数据
        websocket.send(text);
    }
    //onmessage 监听服务器数据推送
    websocket.onmessage = function (evt) {
        msg.innerHTML += evt.data +'<br>';
    };
</script>
</html>
```

4. 在服务器命令行中运行服务端脚本文件

```
php server.php

```

5. 在浏览器打开多个wechat.html页面就可以群发送消息，多个页面都能发送接收。
