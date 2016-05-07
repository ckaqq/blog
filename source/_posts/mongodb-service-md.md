---
title: Windows下Mongodb的配置与使用
date: 2016-05-07
tags:
- Mongo
categories:
- 数据库
---

### 前言
虽然教程网上一搜一大把，不过我还是小结一下吧，作为我的学习笔记

### 安装与启动
1. 下载并安装[MongoDB](https://www.mongodb.com/)，我这里的安装路径为`D:\Program Files\MongoDB\`，版本为`3.2.0`
2. 为了以后方便使用将`D:\Program Files\MongoDB\Server\3.2\bin`加入环境变量
3. 新建`data\db`文件夹用来存放数据库
4. 运行
```shell
mongod --dbpath "D:\Program Files\MongoDB\data\db"
```

### 加入Windows服务
1. 新建`data\log`文件夹用来存放日志
2. 新建`mongo.config`并写入
```
dbpath=D:\Program Files\MongoDB\data\db\
logpath=D:\Program Files\MongoDB\data\log\mongo.log
```
3. 用管理员身份运行cmd并执行命令
```
mongod --config "D:\Program Files\MongoDB\mongo.config" --serviceName MongoDB -install
```

### 配置权限
1. 添加管理员帐号，cmd执行mongo
```shell
# mongoDB 3.0 createUser
db.createUser({user:"admin",pwd:"admin",roles:[{role:"userAdminAnyDatabase",db:"admin"}]});
```
2. 删除掉原来的MongoDB服务
```shell
sc delete MongoDB
```
3. 重新创建Windows服务，加入--auth参数
```
mongod --config "D:\Program Files\MongoDB\mongo.config" --auth --serviceName MongoDB -install
```

### 其他
* 启动MongoDB：net start MongoDB
* 停止MongoDB：net stop  MongoDB
* 删除MongoDB：sc delete MongoDB

### 参考资料
* [windows下MongoDB的安装及配置](http://jingyan.baidu.com/article/d5c4b52bef7268da560dc5f8.html)
* [mongodb的安装以及加入服务启动项（windows）](http://jadethao.iteye.com/blog/1988515)
* [mongoDB 3.0 安全权限访问控制](http://www.ttlsa.com/mongodb/mongodb-3-0-security-permissions-access-control/)
* [MongoDB设置访问权限、设置用户](http://www.cnblogs.com/zengen/archive/2011/04/23/2025722.html)
