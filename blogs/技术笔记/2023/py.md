---
title: Python学习笔记
date: 2017-08-24
tags:
 - 编程开发
categories:
 - 技术笔记
---


## 创建Django的新项目

### 1·创建虚拟环境

cd myproject/

pip3 install virtualenv   
virtualenv venv   
source venv/bin/activate   
复制粘贴 vim requirements.txt   
pip3 install -r requirements.txt      
deactivate

### 2·创建新项目

在虚拟环境的目录下source venv/bin/activate   
django-admin startproject mysite   
进入到项目目录   
python3 manage.py migrate   
python3 manage.py runserver

### 3·数据库配置

打开docker的数据库   
docker pull mysql   
docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d -p 3306:3306 mysql:latest

在settings中配置数据库	     
'ENGINE': 'django.db.backends.mysql',   
'NAME': 'test',   
'USER': 'root',   
'PORT': 3306,   
'HOST': '127.0.0.1',   
'PASSWORD': '123456',

在init文件中加入   
import pymysql   
pymysql.install_as_MySQLdb()


创建管理员用来管理数据库   
python3 manage.py createsuperuser --username=admin --email=admin@email.com

### 4·具体开发过程

按照app，models，view，url的顺序依次创建保存

改变了数据库以后要进行新的数据迁移   
python3 manage.py makemigrations   
python3 manage.py migrate   
python3 manage.py runserver

### 5·打包和部署

原理是创建一个镜像，将依赖包和环境的配置都写进镜像中   
pip freeze > ./requirements.txt 首先在项目目录下生成依赖包文件   
vim Dockerfile 项目下生成docker文件

### 6·使用shell文件快速启动

在同目录下创建文件 open run.sh   
加入#!/bin/bash，加上一行空行，输入命令，最后加上空行   
chmod u+x run.sh 来修改执行权限   
在目录下执行 ./run.sh 就可以

### 7·git的使用方法

创建本地仓库，在同目录下git init   
git add . 添加文件到暂存区   
git commit -m ‘提交说明’ 将修改后的文件统一提交到分支

在github创建新的仓库，复制仓库地址   
git remote add origin 远程仓库地址 将本地git连接上github   
git push -u origin master 上传github   
若有多个版本，先git pull 再进行git push

git remote rm origin 先删掉远程地址   
版本回退，在git端的操作   
git log 查看提交的次数   
git reset  HEAD^ 回退到上一个版本 ^^是两个    
（reset是直接删除了之后的版本，慎用）

版本反回退   
git reflog查看操作的版本编号   
git reset  1094a 可以回退到当前版本

### 8·具体功能的实现

实现数据的增，删，改，查

python3 manage.py dumpdata appname > appname_dump.json   
实现数据库的json格式导出

如何配置pycharm   
1·preferences   
2·interpreter   
选择存在的环境即可   
   
   
   