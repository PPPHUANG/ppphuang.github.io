---
layout: post
title: "Git使用笔记"
date: 2017-08-24
description: "Git使用方法总结"
tag: 工具
---

### Git安装

1. 打开Git官方网站下载适合自己电脑版本的Git安装包。[点击下载](https://git-scm.com)
2. 点击安装包默认安装（安装位置可以自选，其他安装选项默认即可）；
3. 安装完成之后桌面右键点击出现`Git Bush Here`,`Git GUI Here`，则Git安装成功。`Git Bush Here`是在此位置启动命令界面的Git客户端,`Git GUI Here`是在此位置启动图形界面的Git客户端。推荐使用命令界面的客户端，使用常用的几个GIt命令，即可简单方便的使用Git来进行版本控制。

### 拉取远程库里的文件（GitHub为例）

1. 在想要拉取文件的文件夹邮件点击选择`Git Bush Here`，此时会出现一个命令框。
2. 在Github上复制你要拉取远程库的地址，例如：`git@github.com:PPPHUANG/ppphuang.github.io.git`
3. 在Git命令界面 输入以下命令,回车之后就会自动从远程库里拉取对应地址的文件了。
```
git clone git@github.com:PPPHUANG/ppphuang.github.io.git
```
### 本地提交文件到远程库 

1. 第一次使用Git的时候配置用户全局信息，命令如下：
```
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```
2. 生成秘钥，执行如下命令：
```
ssh-keygen -t rsa -C "你的邮箱"
```
3. 查看并复制秘钥，执行如下命令：
```
cat ~/.ssh/id_rsa.pub
```
4. 在GitHub上登录，到你的设置里添加刚刚复制的秘钥。
5. 在本地`clone`这个远程仓库的代码。修改本地代码之后执行以下命名查看代码文件状态（此时修改的代码在工作区）：
```
git status
```
执行以下命令将工作区的代码添加到暂存区：
```
git add filename  //filename是你要添加到暂存区文件的名字
git add . //添加工作区所有修改的文件到暂存区
```
执行以下命令将暂存区的文件添加到本地仓库：
```
git commit -m '提交备注'
```
执行以下命令将本地仓库的文件提交到远程仓库：
```
git push
```
若提交不上去，可能是远程仓库的提交次数领先本地仓库，需要执行以下命令来同步：
```
git pull
```
成功之后，再次执行：
```
git push
```

### 分支概念

1. 查看分支：
```
git branch //查看本地分支
git branch -r //查看远程分支
git branch -a //查看所有分支
```
2. 创建分支,切换分支：
```
git branch branchname //branchname为你要创建的分支名称
git branch checkout branchname //branchname为你要切换到的分支名称
git checkout -b branchname //创建并切换到branchname分支
```
3. 合并某分支到当前分支
```
git merge branchname //合并branchname到当前分支
```
4. 删除分支
```
git branch -d branchname  //删除已经合并的branchname分支
git branch -D branchname //强制删除未合并的分支
```

### 冲突
1. 冲突一般产生在合并分支的时候，当两个分支同时对同一文件的同一部分代码修改的时候时候，自动合并分支时会产生冲突，需要手动合并分支。
2. 手动修改之后再次提交即可解决。

### 说明
1. 在本地切换分支时，文件系统里的文件内容会自动改变成当前分支的内容。
2. 当在一个分支里修改了文件，需要提交到本地仓库之后才能切换到其他分支，否则分支里的修改就会丢失。
3. 如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令:
```
git branch --set-upstream branchname origin/branchname
```
4. 拒绝合并无关的历史
```
git pull origin master --allow-unrelated-histories
```
5. 想要为此分支创建跟踪信息：
```
git branch --set-upstream-to=origin/<分支> master
```
6. 删除远程主机
```
git remote rm origin
```
7. 添加远程主机 
```
git remote add origin github地址
```
