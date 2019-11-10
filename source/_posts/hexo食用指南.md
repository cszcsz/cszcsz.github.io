---
title: hexo食用指南
date: 2019-08-26 23:30:36
categories: 博客搭建问题
tags: [Hexo]
keywords: Hexo, Blog
description: 生命在于折腾，又把博客折腾到Hexo了。给Hexo点赞。
---

## 1.基本命令

1. `hexo new "新文章标题"`  &emsp;新建文章   
2. `hexo new page "页面名称"`&emsp;新建页面
3. `hexo clean` &emsp;清除缓存
4. `hexo g`&emsp;生成静态网页
5. `hexo s`&emsp;启动本地服务器并监听变化自动更新显示
6. `hexo d` &emsp;部署

  

## 2.发布博客

执行`hexo clean`、`hexo g`、`hexo d`来发布博客

我将这三个命令写到了deploy.sh这个脚本文件中，以后部署只用执行脚本`sh deploy.sh`就可以啦~



## 3.日常备份

执行`git add .`、`git commit -m ""`、`git push origin hexo`来备份

（注：我的是master分支用来放public里的页面文件用于展示，hexo分支用来备份源文件）

​    

  



<!--more-->

## 4.恢复

电脑重装后或想在其他电脑上修改博客步骤：

1. 安装git
2. 安装Node.js
3. 执行`git clone -b hexo git@github.com:cszcsz/cszcsz.github.io.git`  (注：这里只克隆hexo分支)
4. 在项目文件夹内执行如下命令：`npm install hexo-cli -g`、`npm install`、`npm install hexo-deployer-git`
5. 记住：hexo分支用于备份源文件，master分支用于存放public文件夹里的内容



补充操作：添加ssh-keys

1. 执行`ssh-keygen -t rsa -C "yourname@email.com"`
2. 用户文件夹下的.ssh目录会生成id_rsa和id_rsa.pub两个文件，其中id_rsa是私钥，id_rsa.pub是公钥
3. 登录github，在设置里面new SSH key，在key文本框里粘贴公钥id_rsa.pub文件的内容
4. 可以用`ssh git@github.com`来验证连接



**配置过程中可能遇到的问题：**

**问题1：**

​	提示`TypeError: can't read property count of undefined`且错误是在`hexo-baidu-url-submit`包中

解决方法：删除该包即可`npm uninstall hexo-baidu-url-submit`



  


  

## 5.附hexo项目文件说明

1. `_config.yml`站点的配置文件，需要拷贝；

2. `themes/`主题文件夹，需要拷贝；

3. `source`博客文章的.md文件，需要拷贝；

4. `scaffolds/`文章的模板，需要拷贝；

5. `package.json`安装包的名称，需要拷贝（如果有`package-lock.json`文件也一并上传，作用是控制依赖包版本号）；

6. `.gitignore`限定在push时哪些文件可以忽略，需要拷贝

7. `.git/`主题和站点都有，标志这是一个git项目，不需要拷贝；

8. `node_modules/`是安装包的目录，在执行`npm install`的时候会重新生成，不需要拷贝；

9. `public`是`hexo g`生成的静态网页，不需要拷贝；

10. `.deploy_git`同上，`hexo g`也会生成，不需要拷贝；

11. `db.json`文件，不需要拷贝。

    注：不需要拷贝的正是`.gitignore`里忽略的



