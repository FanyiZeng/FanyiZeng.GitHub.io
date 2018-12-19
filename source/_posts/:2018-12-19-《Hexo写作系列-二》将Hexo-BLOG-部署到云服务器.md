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

## 对于没有自己服务器的小伙伴,我们可以使用Git仓库的免费服务

1. 安装 hexo-deployer-git。
```
$ npm install hexo-deployer-git --save

npm WARN deprecated swig@1.4.2: This package is no longer maintained
+ hexo-deployer-git@0.3.1
added 31 packages from 36 contributors and audited 5894 packages in 12.363s
found 1 low severity vulnerability
  run `npm audit fix` to fix them, or `npm audit` for details
```

2. GitHub 创建自己的博客仓库.需要按照特定的格式去命名.`UserName.GitHub.io`
ps:查看本机是否已经生成 ssh 公钥. 将控制台输出的公钥粘贴到 Github->Setting->SSH Key 中
```
$ cat ~/.ssh/id_rsa.pub 
```

3. 将代码使用git进行管理,尝试连接到git仓库. 排除可能的bug
```
$ git init  #初始化
# Initialized empty Git repository in /Users/zengfanyi/Dev/hexo_blog/.git/
# 添加所有资源
$ git add .
# 提交一下
$ git commit -m "init"
# 添加远程仓库地址
$ git remote add orgin git@github.com:FanyiZeng/FanyiZeng.GitHub.io.git 
# 尝试推送
$ git push --set-upstream orgin master #推送到仓库
```

> 如果提示以下类似代码... 那么就是GitHub上的 ssh 公钥没有配置正确. 
> ```
> The authenticity of host 'github.com (13.250.177.223)' can't be established.
> RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
> Are you sure you want to continue connecting (yes/no)? yes
> Warning: Permanently added 'github.com,13.250.177.223' (RSA) to the list of known hosts.
> git@github.com: Permission denied (publickey).
> fatal: Could not read from remote repository.
> 
> Please make sure you have the correct access rights
> and the repository exists.
> ```

4. `_config.yml` 文件的配置

```YMAL
deploy:
  type: git
  repo: git@github.com:FanyiZeng/FanyiZeng.GitHub.io.git
  branch: master
  message: update_Ewan
```

--- 

## 想要将BLOG放在自己服务器上,可以使用NGINX服务

- 首先我们在服务器给Hexo创建一个专属账户. 仅仅用于 `BLOG`.(可选)
- 然后我们将使用 Rsync 命令,使用 ssh 自动登录到服务器.快速部署
    - 参考文章[Hexo 之使用 Rsync 进行部署](https://www.practicemp.com/2018/08/hexo-deployer-rsync.html)
    - 
以及[带你跳过各种坑，一次性把 Hexo 博客部署到自己的服务器](https://juejin.im/post/5b70d68ae51d45665d383281)

1. 在服务器开设新用户. 并配置ssh登录 / 尝试登录
2. 配置 deploye 选项 /  `hexo d` 将blog部署到服务器
```
deploy:
  type: rsync
  host: 18.222.198.243
  user: hexo
  root: /home/hexo/SDA_BLOG
  port: 22
  delete: true
  verbose: true
  ignore_errors: false
```
3. 服务器开启 Nginx . 修改配置 . 启动 NGinx . 查看浏览器
> 在部署到服务器执行 `hexo d` 之前. 一定要先执行一次 `hexo g`
> 按照第一篇的流程. 本地随时 `nohup hexo s &` 进行预览.
> 写完后需要发布 则执行 hexo d. 查看服务器上的发布版本~

