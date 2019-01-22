---
layout: post
title: "go main包含多个go文件"
date: 2019-01-22
description: "go main包含多个go文件"
tag: go
---
1. golang main包推荐只有一个main.go文件，这样大家就能按照习惯的方式，go run main.go 或 go build main.go来运行编译项目。

2. 如果main包下有多个go文件，应该使用go run a.go b.go c.go 或 go run *.go来运行，编译同理。

3. 因为mian包里，使用go run main.go，编译器只会加载main.go这个文件，不会加载main包里的其他文件，只有非main包里的文件才会通过依赖去自动加载。所以你需要输入多个文件作为参数。
