---
layout: hexo
title: nginx配置文件
date: 2018-05-21 11:09:43
tags: nginx
---

### nginx文件了解一下

#### 先来了解下nginx

```
Nginx (engine x) 是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP服务器。
Nginx是由伊戈尔·赛索耶夫为俄罗斯访问量第二的Rambler.ru站点（俄文：Рамблер）开发的，第一个公开版本0.1.0发布于2004年10月4日。
其将源代码以类BSD许可证的形式发布，因它的稳定性、丰富的功能集、示例配置文件和低系统资源的消耗而闻名。2011年6月1日，nginx 1.0.4发布。
Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，并在一个BSD-like 协议下发行。
其特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好，中国大陆使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。

```

——来自百度百科

一般来说都是用来做**跨域**处理的，这个地方顺带提一下跨域是什么：

```
	 简单来说：两个url只要协议、域名、端口有任何一个不同，都被当作是不同的域，相互访问就会有跨域问题。
```

#### 然后来了解一下安装部分

Mac：  
1、先安装brew（未安装的自行百度）  
2、在终端里输入指令
```
	brew search nginx
	brew install nginx
```

安装完成  

然后进入 `/usr/local/etc/nginx`目录下，输入nginx或者sudo nginx来启动  
在浏览器中访问localhost:8080成功，说明安装成功了

Windows：  
进入`http://nginx.org/`网址下载安装  
安装完成后进入安装文件夹，双击nginx.exe文件  
在浏览器中能访问成功就说明安装成功了  


#### 配置部分
在终端中进入` /usr/local/etc/nginx `目录，打开目录中的`nginx.conf`文件，文件内容入下：


```

#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
	
	server {
        listen       8000;
        server_name  localhost;

        location / {
            proxy_pass http://localhost:4200;
        }

	location /pc_consumer {
	    proxy_pass http://nginx.com/;
	}
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
}


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
    include servers/*;
}

```

文件中最主要的部分是： 

```
server {
        listen       8000;
        server_name  localhost;

        location / {
            proxy_pass http://localhost:4200;
        }

	location /pc_consumer {
	    proxy_pass http://nginx.com/;
	}
}
```
server http结构下可以有多个server。请求进来 确定 使用哪一个 server由 server_name 确定  
listen 表示监听端口  
server_name 识别的域名，一般可以是localhost  
location 一个server下可以有多个location ，用来匹配 同一个域名下不同uri的访问  
proxy_pass ：转发  后跟系统地址

#### nginx的一些命令
```
start nginx : 启动nginx
nginx -s reload  ：修改配置后重新加载生效
nginx -s reopen  ：重新打开日志文件
nginx -t -c /path/to/nginx.conf 测试nginx配置文件是否正确

关闭nginx：
nginx -s stop  :快速停止nginx
nginx -s quit  ：完整有序的停止nginx
```


写的很粗略，如有不懂请百度	[百度](http://www.baidu.com)


