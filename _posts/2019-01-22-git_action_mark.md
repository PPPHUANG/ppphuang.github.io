---
layout: post
title: "git常用操作"
date: 2019-01-22
description: "git常用操作"
tag: git
---

# 查看历史
### 查看某个文件的历史提交记录
```
git log <filename>
查看文件的详细历史记录
git log -p <filename>
```
### 查看某次提交的具体修改
```
git show <commitID>
或者（跟前一个版本比较不同）
git show <commitID>^!
```
### 以列表形势查看文件历史
```
git blame <filename>
```
### 查看某一行的修改记录
```
git blame -L 100,100 <filename>
git blame -L 100,+10 <filename>
或者通过Log查看
git log -L start,end:<filename>
git log -L 155,155:git-web--browse.sh
```
# 修改
### 文件重命名
```
git mv <old> <new>
```
### 删除文件
```
git rm <filename>
```
### 停止跟踪但不删除
```
git rm --cached <filename>
```
### 修改最近一次提交
```
git commit --amend
```
# 撤销修改
### 撤销工作区中的所有未提交记录
```
git reset --hard HEAD
```
### 撤销工作区中指定文件的未提交记录
```
git checkout -- <filename>
git checkout HEAD <filename>
```
### 撤销指定的提交
```
git revert <commitID>
```
### 选择commit
```
git cherry-pick <commitID>
```
### 可以把本地未push的分叉提交历史整理成直线
```
git rebase
```
### 汇合commit
```
git rebase -i HEAD~~
```
打开文本编辑器，将看到从HEAD到HEAD~~的提交如下图显示。
```
pick 9a54fd4 添加commit的说明
pick 0d4a808 添加pull的说明

# Rebase 326fc9f..0d4a808 onto d286baa
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```
将第二行的`“pick”`改成`“squash”`，然后保存并退出。由于合并后要提交，所以接着会显示提交信息的编辑器，请编辑信息后保存并退出。
### 修改commit
```
git rebase -i HEAD~~
```
打开文本编辑器，将看到从HEAD到HEAD~~的提交如下图显示。
```
pick 9a54fd4 添加commit的说明
pick 0d4a808 添加pull的说明

# Rebase 326fc9f..0d4a808 onto d286baa
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```
将第一行的`“pick”`改成`“edit”`，然后保存并退出。将会显示以下内容，修改过的提交呈现退出状态。
```
Stopped at d286baa... 添加commit的说明
You can amend the commit now, with

        git commit --amend

Once you are satisfied with your changes, run

        git rebase --continue
```
打开sample.txt，适当地修改“commit的讲解”部分。
```
add 把变更录入到索引中
commit 记录索引的状态
pull 取得远端的内容
```
用commit --amend保存修改。
```
$ git add sample.txt
$ git commit --amend
```
现在已经commit，但是rebase操作还没结束。若要通知这个提交的操作已经结束，请指定 --continue选项执行rebase。
```
$ git rebase --continue
```
