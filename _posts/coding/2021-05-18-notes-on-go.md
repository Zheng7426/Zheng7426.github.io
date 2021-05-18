---
layout: post
title: "Golang(Go)笔记"
date: 2021-05-18 00:00:00 -0000
categories: coding 
---

Golang，简称 Go(和围棋的英文一样)，是一门开源的编程语言。谷歌将 Go 专门用于其庞大的服务器网络，而且 Go 也支撑着大部分谷歌云平台的运行。开发者们在软件开发、网页开发、在运营和基础设施团队以及其他情况下使用这门编程语言。Go 是属于原生云基础设施和软件开发的语言。它的程序是由上至下、从左到右运行的，并且会忽视空格。

由于现代计算机只能识别 0 和 1，我们用 Go 写出的代码需要被 _编译器_ 转换为二进制的 0 和 1。被转换之后的代码被称为 _可执行文件(executable)_ 或者二进制文件。然后我们可以运行 可执行文件 以达到我们编写 Go 程序的目的。比如说我们现在有一个名为 app.go 的文件，要想让编译器编译它，可以在控制台输入以下命令：

`go build app.go`

如果此时我们输入 `ls` 查看当前文件夹的文件时，我们会发现多出了一个名为 app 的文件，这个就是编译之后的二进制文件。要运行该二进制文件的话，输入 `./app` 即可。如果使用二进制文件与用户进行交互，访问速度将会提升。然而，如果要对程序有所改动，则需将修改后的源文件再次编译才能知晓改动的效果，这又似乎不是很方便。所幸有一个 `go run` 的命令可以同时编译和执行，比如 `go run app.go` —— 这样我们便可以迅速查看程序的输出，但这个命令并不会生成一个新的文件。

编译器会忽视注释，在 Go 语言中编写注释的方法与 C++、JavaScript 相同，即单行注释用 `//`，多行注释用`/*` 和 `*/`。

每一个 Go 程序的开头都有一个 _包声明(package declaration)_，包声明会告知编译器需要创建的是一个可执行文件还是一个库。与可执行文件不同的是，一个库并不直接运行代码，而是可以被其他程序使用的代码的集合。包声明为 `package main` 的程序会创建一个可执行文件。在包声明之后，通常会有 _导入语句(import statement)_，`import` 关键词让我们能够使用其他的包，导入的包的名称要用双引号括起来。包既可以被逐行导入，亦可被封在括弧中导入：

```golang
import "第一个包"
import "第二个包"
//或
import (
    "第一个包"
    "第二个包"
)
```

在 Python 中导入包时可以为其添上简写(alias)，比如说 `import numpy as np`。同样的，在 Go 中也可以添加简写，简写和包名之间要有空格，方式如下：

```golang
import (
  p1 "第一个包"
  "第二个包"
)
//或 
import p1 "第一个包"
```

_函数_ 是可重复使用的代码区块，在 Go 里是这样定义函数的：

* 函数声明的开头是 `func` 关键词

* `func` 之后跟着的是函数名

* 名称之后则是一对括弧 () 以及一对大括号 {}。类似 JavaScript 中定义函数的形式，但是不用分号结尾。

```golang
package main

import "fmt"

func main() {
    fmt.println("嗨，世界")
}
```

通常来说，函数必须被调用才能运行其代码。然而在 Go 语言中，名为 `main` 的函数是特殊的 —— 当一个 Go 文件有 `package main` 作为其包声明的时候，main 函数会自动运行。

如果不了解上述示例中 fmt 包是做什么的，可以使用 Go 内置的文档系统，在命令行输入 `go doc 包名` 便可以查询特定的文档:

```golang
/*
go doc fmt
或 
go doc fmt.println

import "fmt"

Package fmt implements formatted I/O with functions analogous to C's printf
and scanf. */

/*
go doc time.Now
func Now() Time
    Now returns the current local time. */
```

### 在本地运行 Go

在 Go 的[官网](https://golang.org/) 可以下载适合不同操作系统的安装包。安装包会将 Go 的分发内容装到 /user/local/go 这个路径。/user/local/go/bin 这个目录也应该被添加到你的 PATH 环境变量(这样你就可以在全局使用 Go)。

我们可以输入以下命令来测试 Go 是否已经被成功安装：

`$ go version`

