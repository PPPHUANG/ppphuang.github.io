---
layout: post
title: "go体验RPC"
date: 2019-01-22
description: "go体验RPC"
tag: RPC
---

### 准备工作
1. 安装go环境（gRPC需要go1.6版本以上的环境）
2. 安装gRPC
```
go get -u google.golang.org/grpc
```
墙内不能下载的可以去```https://golangtc.com/download/package```下载压缩包
3. 安装Protocol Buffers v3
```
这里下载压缩包https://github.com/google/protobuf/releases
解压文件
进入目录
./configure
make check
make
make install
```
4. 设置环境变量
```
export PATH=$PATH:$GOPATH/bin
```
### 测试 Protocol Buffers
1. 编写im.helloworld.proto文件
```
syntax = "proto3";

package im;

message helloworld
{
    int32 id =1;
    string str =2;
    int32 opt =3;
}
```
2. 生成im.helloworld.pb.go文件
```
protoc --go_out=. im.helloworld.proto
# 编译当前目录下所有的proto文件
protoc --go_out=. *.proto
```
3. 测试是否能够成功序列化反序列化
```
package main

import (
	"github.com/golang/protobuf/proto"
	"fmt"
	"testrpc/demoproto/im"
)

func main() {
	info := &im.Helloworld{
		Id:1,
		Str:"hellow",
		Opt:2,
	}
	data,err := proto.Marshal(info)
	if err != nil {
		fmt.Println(err)
	}
	newinfo := &im.Helloworld{}
	err = proto.Unmarshal(data,newinfo)
	if err != nil {
		fmt.Println(err)
	}
	if info.GetId() != newinfo.GetId() {
		fmt.Println(info.GetId(),newinfo.GetId())
	}
	fmt.Println(info,newinfo)
}
```
4. 运行看是否按程序设定成功序列化 反序列化
### 编写helloworld的proto文件
```
syntax = "proto3";

package helloworld;

// The greeting service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings
message HelloReply {
  string message = 1;
}
```
5. 生成helloworld.proto文件的go文件
```
protoc --go_out=plugins=grpc:. hellowword.proto
```
### 编写服务端代码
```
package main

import (
"log"
"net"

pb "testrpc/proMes"
"golang.org/x/net/context"
"google.golang.org/grpc"
)

const (
port = ":50051"
)

// server is used to implement helloworld.GreeterServer.
type server struct{}

// SayHello implements helloworld.GreeterServer
func (s *server) SayHello(ctx context.Context, in *pb.HelloRequest) (*pb.HelloReply, error) {
return &pb.HelloReply{Message: "Hello " + in.Name}, nil
}

func main() {
lis, err := net.Listen("tcp", port)
if err != nil {
log.Fatalf("failed to listen: %v", err)
}
s := grpc.NewServer()
pb.RegisterGreeterServer(s, &server{})
s.Serve(lis)
}
```
### 编写客户端代码
```
package main

import (
	"log"
	"os"

	pb "testrpc/proMes"
	"golang.org/x/net/context"
	"google.golang.org/grpc"
)

const (
	address     = "localhost:50051"
	defaultName = "world"
)

func main() {
	// Set up a connection to the server.
	conn, err := grpc.Dial(address, grpc.WithInsecure())
	if err != nil {
		log.Fatalf("did not connect: %v", err)
	}
	defer conn.Close()
	c := pb.NewGreeterClient(conn)

	// Contact the server and print out its response.
	name := defaultName
	if len(os.Args) > 1 {
		name = os.Args[1]
	}
	r, err := c.SayHello(context.Background(), &pb.HelloRequest{Name: name})
	if err != nil {
		log.Fatalf("could not greet: %v", err)
	}
	log.Printf("Greeting: %s", r.Message)
}
```
