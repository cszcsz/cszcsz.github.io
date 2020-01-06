---
title: git常用命令
date: 2019-08-26 23:50:57
categories: git
tags: [git]
---

#### 从github远程克隆项目修改后再推送：

### 常用命令

1. `git clone <url>`&emsp;将项目克隆到本地
2. `git clone -b "branchname" <url>` 克隆远程项目分支到本地
3. `git add . ` &emsp;跟踪所有的文件
4. `git commit -m "commit message"`  &emsp;提交文件到本地版本库
5. `git push orgin "branchname"`  &emsp; 推送到远程仓库分支 
6. `git pull `  拉取远程分支并合并
7. `git status`  &emsp;随时查看状态信息
8. `git branch "branchname"`  创建分支
9. `git checkout -b 分支名`  创建一个新分支并切换到该分支
10. `git diff` 查看更改前后的不同，常在后面接文件名或不接



在工作区(目录)进行文件修改，然后将需要提交的**文件修改**通通放到**暂存区(add)**，最后，一次性**提交暂存区的所有修改(commit)**。

### 版本回退

​	`HEAD`指向的版本是当前的版本，`HEAD^`表示上一个版本

1. `git reset --hard commit_id` 回退到指定提交版本

2. `git log` 查看提交历史，以便回退
3. `git reflog` 查看命令历史，以便重返未来



### 撤销修改

1. `git restore <file>` 丢弃工作区的修改(discard changes in working directory)

2. `git restore --staged <file>` 把暂存区的修改回退到工作区(unstage)

注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！