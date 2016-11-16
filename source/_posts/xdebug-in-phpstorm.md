---
title: PHPStorm 和 Sublime 配置 Xdebug
date: 2016-11-11
tags: [PHPStorm, Sublime] 
categories: PHP
---

### 前言
Xdebug 大法好~

### 安装配置 Xdebug
#### 一、安装
1. 复制 phpinfo() 的内容到 [Xdebug: Support](https://xdebug.org/wizard.php)
2. 按照页面上的提示进行下载和安装

#### 二、配置 php.ini
```shell
[xdebug]
zend_extension="path to xdebug.dll or xdebug.so"
xdebug.remote_enable = 1
xdebug.remote_handler = dbgp
xdebug.remote_host= localhost
xdebug.remote_port = 9001
xdebug.idekey = PHPSTORM
```

#### 三、其他参数
* 禁止对 var_dump 的美化
```shell
xdebug.overload_var_dump=0
```
* 使 var_dump 输出完整变量
```shell
xdebug.var_display_max_depth = -1 
xdebug.var_display_max_children = -1
xdebug.var_display_max_data = -1
```
* 允许多个远程 IP 同时调试（忽略 xdebug.remote_host 参数）
```shell
xdebug.remote_connect_back = 1
```

### PHPStorm 配置 Xdebug
1. Ctrl + Alt + S 打开设置 -> Languages & Frameworks -> PHP -> Debug -> GBGp Proxy，输入 IDE key、域名和端口，注意和 php.ini 一致
![](/img/xdebug-in-phpstorm/xdebug_phpstorm_dbgp.png)
2. 打开设置 -> Languages & Frameworks -> PHP -> Servers，新建一个 Servers
![](/img/xdebug-in-phpstorm/xdebug_phpstorm_servers.png)
3. 点击右上角电话形状的按钮进行监听
![](/img/xdebug-in-phpstorm/xdebug_begin.png)
### Sublime 配置 Xdebug
#### 一、安装 package control
[Sublime Text 3 安装 Package Control](http://jingyan.baidu.com/article/925f8cb817fd49c0dce05653.html)
#### 二、安装 Xdebug Client
1. 使用 package control 安装 Xdebug Client
2. 打开需要调试的项目，点击 Project -> Sava Project As...，修改生成的 .sublime-project 文件
```json
{
    "folders":
    [
        {
            "path": "."
        }
    ],
    "settings":
    {
        "xdebug": {
            "url": "http://localhost/",
            "port": 9001
        }
    }
}
```
#### 三、开始调试
![](/img/xdebug-in-phpstorm/sublime_start_xdebug.png)
#### 四、默认快捷键
* 开始调试 - Ctrl+Shift+F9
* 结束调试 - Ctrl+Shift+F10
* 增加/移除断点 - Ctrl+F8
* 设置条件断点 - Shift+F8
* 执行到下一个断点处 - Ctrl+Shift+F5
* 单步执行 - Ctrl+Shift+F6
* 单步进入 - Ctrl+Shift+F7
* 单步退出 - Ctrl+Shift+F8
* 关闭调试窗口 - Ctrl+Shift+F11
### Chrome 浏览器安装 [Xdebug helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc)
![](/img/xdebug-in-phpstorm/xdebug_helper.png)
### 参考资料
* [Xdebug配置选项](http://www.xingfeilong.cn/article/2013-08-28/86.shtml)
* [PhpStorm 2016.2 Help :: Configuring Xdebug](https://www.jetbrains.com/help/phpstorm/2016.2/configuring-xdebug.html)
* [Xdebug Client](https://packagecontrol.io/packages/Xdebug%20Client)
* [SublimeTextXdebug](https://github.com/martomo/SublimeTextXdebug)
