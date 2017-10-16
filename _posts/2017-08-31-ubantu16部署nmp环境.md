---
layout: post
title: "ubantu16部署lnmp环境"
date: 2017-08-31
description: "ubantu16部署lnmp环境"
tag: ubantu

---

### 1.安装MySQL服务器

`sudo apt-get install mysql-server`

会提示输入密码

### 2.安装PHP和Nginx

1. 添加nginx和php的ppa源

```
sudo apt-add-repository ppa:nginx/stable
sudo apt-add-repository ppa:ondrej/php
sudo apt update
```
2. 安装Nginx
`sudo apt-get install nginx`

安装好nginx，打开浏览器输入 `http://localhost`    看到 Welcome to nginx！ 说明安装成功了。

3. 安装PHP

`sudo apt-apt install php7.0`

4. 安装PHPFastCGI管理器

`sudo apt install php7.0-fpm`

### 3.修改Nginx配置文件

`sudo vim /etc/nginx/sites-enabled/default`

对应部分修改如下


```
 location ~ \.php$ {
                include snippets/fastcgi-php.conf;
        #     # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        }
```

重启Nginx

`sudo service nginx restart`

到此配置文件基本ok了，我们在/var/www/html目录下，新建个index文件测试是否成功
