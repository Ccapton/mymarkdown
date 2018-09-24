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

### 方案二：
**1 安装第三方Web服务器，例如安装nginx**

``` bash
apt install nginx
```
**2 按照ServerStatus-Toyo项目的教程开启服务端**
``` bash
service status-server restart
```
**3 修改nginx配置文件**
``` bash
vim /etc/nginx/nginx.conf
```
或者
``` bash
vi /etc/nginx/nginx.conf
``` 
修改为
``` html
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
        worker_connections 768;
        # multi_accept on;
}

http {

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

            #error_page  404              /404.html;

            # redirect server error pages to the static page /50x.html
            #
            error_page   500 502 503 504  /50x.html;
            location = /50x.html {
            root   html;
            }

            # proxy the PHP scripts to Apache listening on 127.0.0.1:80
            #
            #location ~ \.php$ {
            #    proxy_pass   http://127.0.0.1;
            #}
            # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
            #
            #location ~ \.php$ {
            #    root           html;
            #    fastcgi_pass   127.0.0.1:9000;
            #    fastcgi_index  index.php;
            #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
            #    include        fastcgi_params;
            #}

            # deny access to .htaccess files, if Apache's document root
            # concurs with nginx's one
            #
            #location ~ /\.ht {
            #    deny  all;
            #}
        }


        ##
        # Basic Settings
        ##

        sendfile on;
        tcp_nopush on;
        tcp_nodelay on;
        keepalive_timeout 65;
        types_hash_max_size 2048;
        # server_tokens off;

        # server_names_hash_bucket_size 64;
        # server_name_in_redirect off;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        ##
        # SSL Settings
        ##

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
        ssl_prefer_server_ciphers on;

        ##
        # Logging Settings
        ##

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        ##
        # Gzip Settings
        ##

        gzip on;
        gzip_disable "msie6";

        # gzip_vary on;
        # gzip_proxied any;
        # gzip_comp_level 6;
        # gzip_buffers 16 8k;
        # gzip_http_version 1.1;
        # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

        ##
        # Virtual Host Configs
        ##

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}


#mail {
#       # See sample authentication script at:
#       # http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
#
#       # auth_http localhost/auth.php;
#       # pop3_capabilities "TOP" "USER";
#       # imap_capabilities "IMAP4rev1" "UIDPLUS";
#
#       server {
#               listen     localhost:110;
#               protocol   pop3;
#               proxy      on;
#       }
#
#       server {
#               listen     localhost:143;
#               protocol   imap;
#               proxy      on;
#       }
#}
```
**4 重新加载配置文件,然后重启nginx服务器**
``` bash
nginx -s reload && nginx -s reopen
```

## ServerStatus-Toyo客户端端配置教程

### 参照 https://github.com/ToyoDAdoubi/ServerStatus-Toyo 官网教程
