---
title: Golang学习
author: 雨轩恋
top: false
cover: false
toc: true
mathjax: false
date: 2019-11-01 11:01:15
img:
coverImg:
password:
summary:
    第一个GO程序
tags:
  - hello world
  - GO
categories:
  - GO学习
---

#### hello world

主程序

```
package main

import "fmt"

func main()  {
	fmt.Println("hello ,世界")
}
```

输出结果

![结果](https://img2018.cnblogs.com/common/1471003/201911/1471003-20191110213913050-398519055.jpg)

#### 部署
go程序部署起来也特别方便，go build 文件名即可 会生成一个exe文件。