---
title: 《Hexo写作系列 二》将Hexo BLOG 部署到云服务器
comments: true
date: 2018-12-19 01:42:16
categories: 
    - Hexo
tags: Hexo
---

本文带大家使用最常用的两种部署方式
> 1. Git
> 2. Rsync

- 首先我们在服务器给Hexo创建一个专属账户. 仅仅用于 `BLOG`.
- 然后我们将使用 Rsync 命令,使用 ssh 自动登录到服务器.快速部署
    - 参考文章[Hexo 之使用 Rsync 进行部署](https://www.practicemp.com/2018/08/hexo-deployer-rsync.html)
    - 
[带你跳过各种坑，一次性把 Hexo 博客部署到自己的服务器](https://juejin.im/post/5b70d68ae51d45665d383281)

1. 如何在服务器开设新用户. 并配置ssh登录 / 尝试登录
2. 配置 deploye 选项 /  `hexo d` 将blog部署到服务器
3. 服务器开启 Nginx . 修改配置 . 启动 NGinx . 查看浏览器

执行 hexo d 之前. 一定要 先 hexo g

按照第一篇的流程. 本地随时 `nohup hexo s &` 进行预览.

写完后需要发布 则执行 hexo d

