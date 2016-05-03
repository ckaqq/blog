---
title: 利用Hexo搭建个人博客
date: 2016-05-03
categories:
- 其他
---
### 前言
博客搬家了，正式从新浪云搬到阿里云，从wordpress改为hexo，在此简单记录一下搭建过程


### 准备工作
* 系统：Windows 10
* 工具：
  * Git
  * Node.JS

这些在搭建博客之前就已经安装完毕，故不赘述


### 安装Hexo并建站
``` bash
npm install hexo-cli -g
hexo init blog
cd blog
npm install
```

#### 安装Jacman主题
``` bash
git clone https://github.com/wuchong/jacman.git themes/jacman
```

#### 多说评论显示UA
参考[多说自定义CSS头像和多说评论显示UA](http://wsgzao.github.io/post/duoshuo/)

### 自动部署
阿里云服务器上执行
``` bash
sudo git init --bare blog.git
cd blog.git/hooks
sudo vim post-receive
```
vim写入
``` text
#!/bin/sh
GIT_WORK_TREE=/web/blog/ git checkout -f
```
退出vim后继续执行
``` bash
chmod +x post-receive
sudo chown -R git:git /home/git/blog.git
```
nginx反向代理
``` bash
# 博客
server {
        listen 80;
        server_name www.kchen.cn;
        root /web/blog/;
}
# 不带www的要跳转
server {
        listen 80;
        server_name kchen.cn;
        return 301 $scheme://www.$host$request_uri;
}
```
在本地_config.yml的deploy后面添加
``` text
deploy:
  type: git
  repo: git@kchen.cn:blog.git
```

### 其他
本地预览博客效果
``` bash
hexo server
```
更新远程服务器
``` bash
hexo deploy
```

### 参考资料
* [文档| Hexo](https://hexo.io/zh-cn/docs/index.html)
* [Jacman](https://github.com/wuchong/jacman/blob/master/README_zh.md)
* [HelloDog](http://wsgzao.github.io/)
* [使用Git来部署一个Web站点笔记](http://rmingwang.com/using-git-to-deploy-a-web-site.html)