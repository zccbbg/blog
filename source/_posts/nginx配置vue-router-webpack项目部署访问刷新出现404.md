---
title: nginx配置vue-router+webpack项目部署访问刷新出现404
date: 2018-08-13 23:17:46
tags: nginx
categories: devops
---

项目使用的是vue2.0,vue-route,webpack打包 

项目部署使用的nginx 

问题描述： 

正常首页不加index可以访问 

如：浏览器输入192.168.0.251可以正常访问并返回 
![1](1.png)

但是当按下F5或者刷新页面时就出现如下404错误 
![2](2.png)

这还是不是最明显的最明显的如这种目录192.168.0.251/user 

基便不刷新而只是访问依然是报的404

## 原因
打开开发包我们会看到除了index.html根本就不存在如上的index和user文件，当然是找不到的因此就返回了404错误。

## 解决思路

因此找到原因就好办了，只需要当服务器发现客户端发来的url时就重定向（服务器重定向）到默认的index.html文件内容并返回给客户端，这样就实现了它的自身的路由功能。

但是也会出现一下问题，比如多个项目使用同一个域名和ip地址的情况，虽然vue项目可以正常访问，但是其他类型的项目显然会问题（一直停留在首页不动，至少是在视觉上不动）。这时就需要根据不同的项目名设置不同的规则，这个内容请参考另外的的文章：nginx配置多个项目（太简单了没写，自行百度）

```
server {
    listen       80;
    server_name  zq.xxx.com;
    root  /opt/xxx/dist/;
    index  index.html;
    location / {
       try_files $uri $uri/ /index.html last;
        index index.html;
    }
}
```