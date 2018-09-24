---
title: 2018-9-24未命名文件 
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---
### 2018/9/24
### 项目：ServerStatus-Toyo
**介绍：云探针、多服务器探针、云监控、多服务器云监控**

**演示：http://111.230.231.107:8888**

**项目地址： https://github.com/ToyoDAdoubi/ServerStatus-Toyo**

**演示环境：Ubuntu 16.04.5 LTS x86_64 (腾讯云主机)**

### 请在root用户下执行全部命令

## ServerStatus-Toyo服务器端配置教程

### 方案一：
**按照ServerStatus-Toyo项目的教程按照全部依赖项目**

### 方案二（当方案一的默认Web服务出错并无法使用时请选择此方案）：
**先安装好ServerStatus-Toyo服务端程序**
**1 按照ServerStatus-Toyo项目的教程开启服务端**
``` bash
service status-server restart
```
**2 安装第三方Web服务器，例如安装nginx**

``` bash
apt install nginx
```

**3 修改nginx配置文件**
``` bash
vim /etc/nginx/nginx.conf
```
或者
``` bash
vi /etc/nginx/nginx.conf
``` 
关键部分修改为
``` html
server {
            # 修改端口，注意安全组配置要开启此端口下的TCP/UDP传输权限
            listen       8888;
            # 服务器名随意
            server_name  capton;

            #charset koi8-r;

            #access_log  logs/host.access.log  main;

            #我们要修改的Web主目录路径，设为 /usr/local/ServerStatus/web
            location / 
                root   /usr/local/ServerStatus/web;
                index  index.html index.htm;
            }
```
**4 重新加载配置文件,然后重启nginx服务器**
``` bash
nginx -s reload && nginx -s reopen
```

## ServerStatus-Toyo客户端端配置教程

### 参照 https://github.com/ToyoDAdoubi/ServerStatus-Toyo 官网教程
