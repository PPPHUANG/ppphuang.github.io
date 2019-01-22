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

