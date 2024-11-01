---
title: Go学习笔记
date: 2017-08-24
tags:
 - 编程开发
categories:
 - 技术笔记
---


# go语言学习笔记

## 基本语法

### 1·声明变量：
声明类型：var number int = 10      
不声明类型：number := 10

### 2·函数的声明：
func max (x,y int) int {   
}     
func swap (x, y string) (string string){   
}       
无需分号，但需要大括号，介于java和Python之间     
需要输入参数和返回参数的类型，可使用多个参数

### 3·for循环：
for 条件 {   
}     
和python类似，可以用i指定循环次数     
使用range关键字返回索引和值     
for i,num := range nums     
for k,v := range kvs     
for i,c := "string"     
for可以和break和continue共同使用

### 4·数组的定义和初始化
也是可以分为是否声明类型     
var number [3]int = [3]int {1,2,3}     
number := [4] int {1,2,3}     
（：代替了var）

### 5·指针
指针需要声明变量     
var a int = 10     
var ptr \*int = &a       
ptr指的是a的地址       
\*ptr指的是a的值       
&和\*是对立的，给结构体加*指的是值     
空指针是nil

### 6·结构体
type Book struct{     
name string     
age int     
}     
Book{name:"akun", age: 10}       
直接进行创建       
var myBook Book      
myBook.name = "akun"     
myBook.age = 10     
先声明再创建     
myBook.age = 10     
直接引用

### 7·切片
没有长度的数组声明     
var s int[] = []int{1,2,3}     
var s = make([]int,0,5) 类型，长度，容量     
长度是切片元素的个数，容量是切片第一个元素到数组最后一个的长度     
arr:=[5]int{0,1,2,3}     
var s = arr[1:3] [1,2] 前算后不算     
var s = arr[;3] [0,1,2] 从零开始     
var s = arr[1;] [1,2,3] 到数组末尾

### 8·map
键值对   
m := map[string]string{"france":"paris"}     
m := make(map[string]string)     
m["france"] = paris

### 9·强制类型转换
`var num int = 8`     
`num2 = float32(num)`   
不支持隐式类型转换，均需要声明




## 学习记录

###gin框架下载安装   
go env -w GO111MODULE=on      
go env -w GOPROXY=https://goproxy.cn,direct 先挂代理     
sudo go get -u github.com/gin-gonic/gin 使用sudo进行下载     
选择工作目录，创建文件，在goland中运行     
go env查看相关信息     
GOROOT="/usr/local/go"     
GOPATH="/Users/zhangyukun/go"     
用来访问和修改环境变量文件     
vim ~/.bash_profile     
source ~/.bash_profile

### goland的配置

1·自己创建三个目录，bin，pkg，src，   
要有一个main目录放到src下，main函数放到main目录下       
2·配置，选择go，build，选择directory，工作目录都选到main的文件夹   
最后将同级的go文件的包名都改成main     
3·sudo go run main.go 启动服务

### 阶段性测试任务
完成一个gin的demo，成绩管理系统，增删改查     
增加(Create)、检索(Retrieve)、更新(Update)和删除(Delete)     
上午：先实现简单的一项     
下午：将各种功能补充完整，加入日志中间件检查等功能

### restful api架构
名称：表现状态转化     
定义：使用四个请求方法传递信息 GET POST PUT DELETE     
在服务端和客户端进行通信     
可以使用多种形式，通常使用JSON格式

### 创建gin新项目流程
编写顺序     
调用结构：不同的部分如何相互调用，目录的格式     
创建数据：创建数据表gorm，批量插入数据     
接收请求：获取不同请求的参数     
返回响应：根据参数对数据表进行增删改查的处理     
分配路由：给不同的请求不同的路由

### 编程习惯：
配置文件集中书写，方便维护和修改     
先搭建基本框架，再对于每一个步骤进行检验和容错

### 学习经验
1·从最小的项目开始做起，清晰地明白每一条语句的含义     
2·从完整的现成的项目开始学起，不要试图自己去拼装，而是做删减     
3·先理清思路，再独立模拟一遍     
由简单到复杂     
从每一个函数，每一个语句开始，把容错全部去掉     
自己独立理解每一条语句

### gin项目管理包依赖

1·创建文件夹，目录和文件      
2·mod管理      
`go mod init modulename`      
`go mod tidy `


### 开发经验

突然就运行不了该怎么办      
使用log记录错误 log.Println(err)

用git拉取最新的项目代码      
`git pull origin master`

gin的包管理mod      
在文件夹下 权限不够前面加上sudo      
`go mod init modulename `     
`go mod tidy`

gin去红色警告      
goland的设置——preferences——go——go modules——打上勾选择groxy

gin的configration      
选择go build      
选择directory——两个路径均选择main.go所在文件夹下      
去掉-i参数

gin测试单个函数的时候      
在main里以调用函数的形式测试      
库中的函数跑起来也很费时间

随着框架变得复杂，难度呈几何级上涨      
每一个接口和库函数都需要学习和熟悉掌握

### 常见错误：

* 不要把接口文档中参数也写到服务器的路由中
* 在用BindJSON绑定时，要注意结构体和发送的数据格式
* 尤其注意不要轻易相信接口文档的数据
* 改完没有重新biuld
* 改完没有重新运行
* 定向少了一个/


### curl的测试语句

新建   
`curl -X POST 'http://127.0.0.1:9000/v1/post' -d '{"id":13,"name":"11","score":"23","status":true,"like":1}' `

查询单条   
`curl -X GET 'http://127.0.0.1:9000/v1/get/single/?id=11'  `

查询全部   
`curl -X GET 'http://127.0.0.1:9000/v1/get/all'   `

更改   
`curl -X POST 'http://127.0.0.1:9000/v1/update/?id=2' -d '{"id":2,"name":"kun","score":"99","status":true}'   `

删除   
`curl -X GET 'http://127.0.0.1:9000/v1/delete/?id=11'  `

玫瑰接口的测试文件   
`curl -X POST 'http://127.0.0.1:9000/v1/islike/' -d '{"name":"16"}' `

### 测试的三种方式
postman     
python脚本     
命令行发送

### postman使用指南
1·方法 GET POST     
2·参数 GET的参数是在params里     
POST的参数在params里     
请求的内容如果是application/json的话     
选择Body中的raw，选择JSON     
在输入框中输入自己的数据


### 玫瑰项目经验
写接口     
关键在于，理解功能     
和哪些数据表关联，前后顺序是什么，需要调用到哪些文件     
这些需要自己去读懂     
示例   五张表   auth，chats，msgs，users，migrations   
一个user可以有多个chat，一个chat相当于选择的一个角色，chat包含user_id   
一个chat可以有多个msg，一个msg相当于对话中的一条语句，msg包含chat_id    
msg id chat_id-->chat id user_id-->user auth_code

简单接口测试跑不通，按照流程依次排错   
发送的不知道是否接收到，没反应   
执行的没反应不知道是哪里的问题   
说明这部分代码有问题   
干脆全部换掉

不知道问题在哪里，多一个何少一个&   
用new还是用var   
用score还是“score”很迷茫

插入mysql的语句    
INSERT INTO meta_msgs    
VALUES   
(1, '1', NOW(), NOW(), 1, 'huihua', 1, 'zh_hans', '12');

没办法测试，因为有各种关联   
需要从母表开始建立

排查错误安插fmt打印各个阶段的值，看走了那个分支   
通常都是细节的语法错误   
先将问题分区，再一句话一句话看

## 一些知识

### 网络编程
通过互联网协议   
主要是五层结构   
物理层，光纤，无线电，代表0，1   
数据链路层，数据包，帧，表头和数据，对数据划分   
网络层，分为MAC地址-网卡，IP地址——网络划分   
同一网络通过广播，不同网络通过路由   
传输层，端口，规定一个电脑下不同程序接收数据包的位置，TCP协议   
应用层，http协议，决定一个程序下不同数据传输的格式

### socket：
一个API,封装了TCP/IP协议，服务端和客户端分别调用可   
实现TCP的通信   
websocket：单个TCP实现双端通信   
http：客户端和服务端分别调用可以实现http通信   
重点在于掌握调用的概念和语法

### 跨域
前后端分离，不在同一个协议，同一个域名，同一个端口   
加入一个中间件，允许跨域请求   
接收时默认跨域调用中间件，   
获取参数的代码可以用格式转化   
要验证跨域，需要自己写一个简单的前端来发起请求

### yaml和ini
配置文件   
文件保存配置信息   
在配置函数中导入文件   
引用信息

### cookie
服务器发送给客户端   
客户端请求时携带cookie   
先登录/login，再使用/home

### 身份认证
authcode主要用于身份认证   
go需要自己写用户登录程序   
验证相关   
需要自己造轮子

### 埋点
收集产品运营过程的数据   
确定在什么地方设置对什么数据的埋点   
脚本文件获取埋点信息

### 思路
理解流程和元素   
框架在于知道框架省略的步骤   
能简单模拟框架的步骤   
具体的语言的区别在于调用语法   
语法只是一种规定，关键在于知道修改哪些参数   
语言区别在于语言特性，会决定设计模式和运行性能


### 常用网址：
1·`http://www.topgoer.com/%E5%85%B6%E4%BB%96/Swagger.html   `
swagger--go语言中文网

2·`https://gin-gonic.com/zh-cn/docs/   `
gin框架

3·`https://www.kancloud.cn/shuangdeyu/gin_book/949414  `
gin中文文档

4·`https://youtu.be/YFl2mCHdv24  `
docker的video

5·`https://yeasy.gitbook.io/docker_practice/install/mac   `
docker的文档

6·`http://www.yunweipai.com/34731.html   `
docker的文档

### redis相关操作
非关系型key-value的内存数据库   
用于数据缓存

mac安装redis   
`brew install redis  `

配置环境变量   
`vim ~/.bash_profile   `

加入环境变量   
redis环境变量   
`export PATH=$PATH/usr/local/opt/redis/bin   `

使环境变量生效   
`source ~/.bash_profile   `

启动服务   
`redis-server /usr/local/etc/redis.conf  `
一般用不成   
`brew services start redis  `
所以用这个   
停止服务   
`brew services stop redis   `

打开客户端   
redis-cli   
插入键值对   
set name hestyle   
get name   
退出   
exit

常见错误：   
出现找不到包的问题   
通过命令行的go mod   
来下载包就可以   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   