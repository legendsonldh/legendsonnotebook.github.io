# Hole in Go

在此记录学习Golang中时遇到的坑

> Q1：go包管理代理地址: https://proxy.golang.org 在国内无法访问的问题

A: 换一个国内能访问的代理地址：https://goproxy.cn

执行命令：
```bash
go env -w GOPROXY=https://goproxy.cn
```
参考链接：https://www.lakeui.com/p/611d103a6c192


> Q2: 在go引入同目录下包时执行报错：`change.go:12:2: package filepath is not in GOROOT`

该问题是由于没有设置Go包的起始搜索路径导致的，

`set GO111MODULE=off` and `set GOPATH` to desired location is also working good.

```bash
go env -w GO111MODULE=off
set GOPATH=<你的项目文件夹>
```

参考链接：https://stackoverflow.com/questions/68693154/package-is-not-in-goroot

> Q3: 解决go: go.mod file not found in current directory or any parent directory； see ‘go help modules‘

`go.mod`是一个记录go模块包的文件，这里说的意思是当前目录下并没有该文件，于是我们新建即可，这一包管理器相当于是在局部管理所有的Go包

```bash
go env -w GO111MODULE=on
go mod init ...
```