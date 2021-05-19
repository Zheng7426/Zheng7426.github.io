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

当你的代码从别的模块导入包的时候，你通过你代码自身的模块来管理这些依赖。这个用于管理依赖的模块由 go.mod 文件定义，该文件会追踪提供包的模块。这个 go.mod 文件(类似 package.json 或 Gemfile)与你的代码在同一个目录下，亦存在于你的源代码仓库。

你可以运行 `go mod init 模块路径` 来创建一个 go.mod 文件。比如：

`go mod init example.com/hello`

fmt 属于 Go 的[标准库](https://golang.org/pkg/#stdlib)里的包，倘若我们需要调用一个外部的包，比如说这个包名为 "rsc.io/quote"，它可以给我们发回一句名言。我们先用下列代码将其导入：

`import "rsc.io/quote"`

然后输入 `go mod tidy`，这个命令类似 `npm install` —— Go 将会找到这个包，并且将其作为依赖下载，使得程序可以顺利执行。同时，Go 也会生成一个用于认证模块的 go.sum 文件。

### 开发一个可供他人使用的模块

Go 的代码汇聚成包，而包则可以汇聚成模块。通常来说，你的模块标注了运行其代码需要哪些依赖，包括 Go 的版本以及所需的其他模块。在一个模块中，你会为了一些特定的、有用的函数而聚敛一个或多个相关的包。

当你为模块增加或改进功能之后，便可以发布该模块的新版本。其他调用了你模块中的函数的开发者可以导入该模块更新后的包，并且在放入生产环境之前对新版本进行测试。

创建一个名为 greetings 的模块的目录：

`mkdir greetings && cd greetings`

创建一个追踪依赖的 go.mod 文件：

`go mod init github.com/具体路径/greetings`

创建一个名为 greetings.go 的文件：

`touch greetings.go`

为这个文件加入下列代码：

```go
package greetings

import "fmt"

func Hey(name string) string {
    message := fmt.Sprintf("嘿, %v. 欢迎!", name)
    return message
}
```

在上述这段代码中，我们首先声明了名为 `greetings` 的包，用于聚敛相关的函数。然后，一个名为 Hello 的函数用于返回打招呼的内容。这个函数接受一个类型为字符串的 `name` 参数。该函数返回的也是字符串。在 Go 这门语言中，一个大写字母开头的函数可以被不在同一个包里的函数调用，这被称为导出名称(exported name)。

我们看到函数的主体中有出现 := 这个运算符，该运算符可以同时声明及初始化一个变量(Go 会根据右边的值来确定该变量的类型)。带 := 的这行代码也可以被写成这样：

```go
var message string
message = fmt.Sprintf("嘿, %v. 欢迎!", name)
```

查看 `fmt.Sprintf` 的文档：

`go doc fmt.Sprintf`

```go
func Sprintf(format string, a ...interface{}) string
    /* Sprintf formats according to a format specifier and returns the resulting
    string. */
```

我们发现 `Sprintf` 函数的第一个参数是个格式字符串，而 Sprint 会将 `%v` 格式动词替换为 `name` 参数的值。第二个参数便是 `name` 参数。

### 从另一个模块中调用之前的代码

创建一个名为 hey 的目录，然后你目前的目录结构看起来会是这样：

```
<根目录>/
 |-- greetings/
 |-- hey/
```

为你即将要创建的 hey.go 文件开启依赖追踪：

`go mod init github.com/具体路径/hey`

创建 hey.go：

`touch hey.go && vim hey.go`

添加以下代码：

```golang
package main

import (
	"fmt"
	"github.com/具体路径/greetings"
)

func main() {
	message := greetings.Hey("荷马")
	fmt.Println(message)
}
```

在环境生产使用的话，你需要从代码仓库发布 greetings 模块，这样 Go 的相关工具才可以找到该模块并下载它。目前我们还没有发布模块，所以暂时可以先对 hey 模块做一些修改，从而让它在本地寻找我们的 greetings 模块。

我们使用 `go mod edit` 来重定向搜寻模块的工具：

`go mod edit -replace=github.com/具体路径/greetings=../greetings`

输入 `go mod tidy` 来找寻本地的模块并将其添加为依赖。然后便可以运行 hey.go 这个文件：

`go run hey.go` 或 `go run .`

### 返回故障、处理故障

故障处理是编程很重要的一部分。我们将会添加一些代码来从 greetings 模块返回一个故障，然后在调用它的模块中进行处理。

* 首先我们导入 Go 标准库中的 `errors` 包，这样才可以调用这个包的 `errors.New` 函数。

* 将 Hey 函数返回的值由 `string` 改成 `(string, error)`，这样它就返回两个值。任何 Go 函数都可以返回多个值。

* 增加一个 `if` 语句来查看 `name` 是否为空，如果是的话则返回一个故障。`errors.New` 函数会返回一个带有你编写的信息的故障。

* 在没有故障的情况下，在返回的第二个值的位置加上 `nil`(意味着没有故障)。

修改后的 greetings.go 文件看起来是这样子：

```go
package greetings 

import "fmt"
import "errors"

func Hey(name string) (string, error) {
	if name == "" {
		return "", errors.New("empty name")
	}

	message := fmt.Sprintf("嘿, %v. 欢迎!", name)
	return message, nil 
}
```

当故障被返回至 hey.go 模块时，我们便需要编写处理故障的代码。

* 首先导入标准库中的 `log` 包，在 `main()` 函数主体中对其进行配置，使得日志信息的开头是 ("greetings: ")，且没有时间戳或者源文件的行数等信息。

* 因为 Hey 返回两个值，我们也在调用该函数时赋两个值，包括 error。

* 将传递给 Hey 的 `name` 参数修改为空字符串，这样你就可以测试故障处理的代码。如果你得到一个故障，`log.Fatal()` 函数会打印出这个故障，并且停止该程序的运行。


```golang
package main

import (
	"fmt"
	"log"

	"github.com/Zheng7426/Golang-practice/greetings"
)

func main() {
	log.SetPrefix("greetings: ")
	log.SetFlags(0)

	message, err := greetings.Hey("荷马")
	
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println(message)
}
```




