---
title: 服务器部署笔记
date: 2017-08-20
tags:
 - 编程开发
categories:
 - 技术笔记
---




### Abstarct：
远程云服务器和本地的linux服务器的操作是一样的  
按照下载依赖包配置环境，拉取项目，运行项目的流程  
部署需要额外的http服务器配置和网关配置  
部署还可以选择docker部署，可以使用docker打包以后上传，然后使用docker启动服务，方便修改维护

### 1·安装docker

`curl -fsSL https://get.docker.com | bash -s docker --mirror aliyun` 安装docker  
`sudo systemctl start docker` 启动docker

### 2·安装mysql和启动mysql

`docker search mysql` 搜索镜像    
`docker pull mysql` 拉取镜像    
`docker images` 显示本地镜像列表  
`docker run -p 3306:3306 --name mysql的name -e MYSQL_ROOT_PASSWORD=123456 -d mysql` 启动本地镜像  
`docker ps` 查看正在运行的mysql  
`docker exec -it 镜像的名字 bash` 进入mysql命令行  
`exit`退出

### 3·理解web服务器

WSGI和uwsgi是两种通信协议  
uWSGI是一种web server服务器，支持多种协议  
协议分为两部分，web服务器和应用服务器  
web server 对接客户端，发送请求，接收响应  
web appliation 对接服务端，接收请求，发送响应  
两者之间由中间件对接  
django一般自带application和server  
通常架构为nginx+uWSGI+django  
前两者均为web server，但Nginx可解决负载均衡，因此搭配使用  
web server：nginx，apache，uWSGI  
两者之间的：Tomcat iis

### 4·理解Nginx

定义：web server，Http服务器，介于客户端和中间件之间  
功能：  
正向代理和反向代理  
正向，VPN，从内网到外网， 多对一，客户端对于服务端未知  
反向，VPN用百度，从外网到内网，一对多，服务端对于客户端未知  
负载均衡  
将请求分配到多个服务器，形成服务器集群  
动静分离  
请求分为静态和动态，静态直接处理，动态转发给服务端

### 5·理解框架

HTML：管理页面内容  
CSS： 管理页面样式，  
JavaScript：管理页面的行为动作  
Bootstrap： 前端框架，响应式设计，移动端优秀  
font awesome： 图标库 为CSS提供丰富的图标  
HTML DOM： 文档对象模型 是HTML和XML的接口，便于访问和操作HTML  
jQuery： JavaScript库，简化事件编程  
Angular JS： 前端框架  
Vue： 前端框架  
React： 前端框架  
Node.js： 运行在服务端的JavaScript  
AJAX： 异步 JavaScript 和 XML，无需全部加载，更新网页信息  
JSON： JavaScript对象表示法，文本数据交换格式  
XML： 可扩展标记语言，用来传输数据  
Servelet： Java的web框架  
SQL： 结构化查询语言  
MySQL： 关系型数据库  
MongoDB： 非关系型数据库  
Redis： 键值数据库

### 6·理解语言

高级编程语言：方便人类阅读
脚本语言：操作自动化

Gg)LAhkyi1Jr
http://101.200.226.58/wp-admin/

plugins
themes

GPU的使用
端口2223
http://10.112.152.226:1357/

cpu是多功能 玛莎拉蒂，一次能拉3位乘客
gpu是专注图形和数值计算 卡车，一次能拉20位乘客，多核并行任务

ssh -p 2223 zhangyukun@10.112.180.165
101.200.226.58

vpn.bupt.edu.cn

分布式

博客的ip  
185.199.111.153  
如果是CNAME的话  
选择常用的名称网址  
如果是A的话  
选择ip网址  
在博客中设置域名  
在云服务中解析网址ip

失败了 没找到原因

本机IP
192.168.0.222