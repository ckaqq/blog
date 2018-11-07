---
title: MAC 下如何快速切换 hosts 并在 Chrome 迅速生效
date: 2018-06-01
tags: [MAC] 
categories: 其他
---

## 前言
在日常开发、测试过程中，可能需要频繁地切换 hosts，可是每次切换 hosts 过程很麻烦不说，还经常会遇到不生效的问题。为了能”优雅”地切换 hosts，下面提供一套在 MAC 下快速切换 hosts 并在 Chrome 迅速生效地一套方案。

## 用到的软件：
* [SwitchHosts](https://github.com/oldj/SwitchHosts)
* [Alfred](https://www.alfredapp.com/)
* [SwitchHosts Alfred Workflow](http://www.packal.org/workflow/switchhosts)
* [DNS Flusher](https://chrome.google.com/webstore/detail/dns-flusher/nbomnjapnclaocillijpceooehonajnk)

## 一、配置 hosts
在 [SwitchHosts](https://github.com/oldj/SwitchHosts) 中提前配置好各种环境下要用的 hosts
![](/img/mac-hosts-switch/config.png)

## 二、快速切换
1. 通过点击顶部菜单栏的图标快速切换 hosts
![](/img/mac-hosts-switch/menubar.png)
2. 通过 Alfred Workflow 实现使用键盘快速切换 hosts
![](/img/mac-hosts-switch/workflow.png)

## 三、在 chrome 中生效
1. 安装插件 [DNS Flusher](https://chrome.google.com/webstore/detail/dns-flusher/nbomnjapnclaocillijpceooehonajnk)
2. Chrome 进入 `chrome://flags/extensions-on-chrome-uirls` 并将 `Extensions on chrome:// URLs` 设置为 Enabled，允许插件操作 `chrome://` 开头的 URL
![](/img/mac-hosts-switch/flags.png)
3. 点击图标![](/img/mac-hosts-switch/extension.png)清除缓存
4. 配置 Chrome 快捷键实现只使用键盘清除缓存，我设置的是 `Command + Shift + K`
![](/img/mac-hosts-switch/shortcut.png)

**至此，一套完整的切换 hosts 方案就完成了，当需要切换 hosts 时，首先使用 `Command + 空格` 呼出 Alfred -> 输入 `swh` 并选择相应配置 -> Chrome 中使用快捷键 `Command + Shift + K` 清除缓存，整个过程只需 2 ~ 3 秒**

## FAQ
1. Q：为什么使用这套方案？
   A：只用键盘操作、快。
2. Q：每次进入 Chrome 都会有 `您使用的是不受支持的命令行标记…` 提示，很烦人怎么办？
   A：退出 Chrome 时不要使用 Command + Q，使用 Command + Shift + W 关闭所有标签页，因为 Chrome 并没有完全退出，所以下次进的时候就不会有提示了。
3. Q：为啥不用 [Awesome Host Manager](https://chrome.google.com/webstore/detail/awesome-host-manager/pikaoeecieigblebdddckmlegonlogha?hl=zh-CN)、[Host Switch Plus](https://chrome.google.com/webstore/detail/host-switch-plus/bopepoejgapmihklfepohbilpkcdoaeo)…之类的 Chrome 插件？
   A：和必备插件 [Proxy SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif?hl=zh-CN) 冲突。
