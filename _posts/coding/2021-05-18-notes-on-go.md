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

编程中的 _函数_ 与其在数学中的定义不同，它指的是可重复使用的代码区块。它亦可以返回数据给程序的其他元素，如果有要返回的值的话，在定义函数的时候要在函数名、参数名之后标注返回值的类型。在 Go 这门语言中，每一个函数都会生成自己的 _作用域(scope)_。作用域指的是值或者函数被定义、可被访问的空间。作用域分为全局作用域和本地作用域。

在 Go 里是这样定义函数的：

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

采用 `defer` 关键词可以使一个函数在载体函数运行到末尾时才调用。

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

"fmt" 可以理解为 formatter 的简写。`fmt.Println()` 会在打印完内容之后另起一行，而 `fmt.Print()` 就不会有这样默认的行为。若要连接(concatenate)字符串及变量，我们可以在这两个函数中使用逗号分隔。

`fmt.Printf()` 让我们往字符串中的 placeholder 插入值：

```go
yourAnswer := "B"
fmt.Printf("Your answer is %v .", yourAnswer)
// 输出: Your answer is B
```

`fmt.Sprintf()` 与 `fmt.Printf()` 很相似，主要的区别在于 `fmt.Sprintf()` 返回其值，而不是将其打印出来。

在 Go 语言中，以 % 开头的 %v 被称为动词(verb)。下表列出了一些常见的动词：

动词名称 | 释义
------ | ------
%v | 默认格式下的值，会被紧随其后的变量名依次替换
%#v | 在 Go 语句下值的表征方式
%T | 在 Go 语句下值的类型的表征方式
%d | 十进制的数字
%f | 小数点精确位数，如 %.2f (7.77)
%% | 一个字面的百分号(%)

若想要获取用户的输入，可以查看以下示例：

```go

fmt.Println("今天天气怎么样?")
var weather string
fmt.Scan(&weather)
fmt.Printf("原来今天天气是 %v。", weather)

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

故障处理是编程很重要的一部分。我们将会添加一些代码来从 greetings 模块返回一个故障，然后在调用它的模块中进行处理。故障信息首先会显示文件名，然后故障出现的行，再然后是列，最后才是说明故障原因的信息。

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

### 返回一个随机的招呼语

我们将对之前的代码作出如下修改，使得 greetings 模块不再返回单句招呼语，而是返回几句预先定好的招呼信息之一。我们会使用一个 Go slice。一个 slice 的大小可以在添加或剔除元素时动态地改变，除此之外它就像数组一样。

* 首先，额外导入 `math/rand` 和 `time` 包。创建一个用当前的时间 seed `rand` 包的 `init()` 函数。在程序启动时，Go 会在全局变量初始化之后自动执行 init 函数。

* 添加一个返回随机选择的招呼语的 `randomFormat` 函数。注意，`randomFormat` 是小写字母开头，所以只有它自己包里的代码才可以访问它，而不像 `Hey(name string)` 这个函数一样可以被导出。在这个函数主体中，声明一个带有 3 个信息格式的格式 slice。当你声明一个 slice 的时候，忽略其方括号中的大小，像这样：[]string。这将会告诉 Go 在 slice 之下数组的大小可以被动态改变。

* 使用 `math/rand` 包来生成一个随机的数，用于从 slice 中选择一项元素。

* 在 `Hey` 函数中，调用 `randomFormat` 函数获取一个返回的格式信息，然后用该格式和 `name` 值一起创建该信息。

```golang
package greetings 

import (
	"fmt"
	"errors"
	"math/rand"
	"time"
)

func Hey(name string) (string, error) {
	if name == "" {
		return "", errors.New("empty name")
	}

	message := fmt.Sprintf(randomFormat(), name)
	return message, nil 
}

func init() {
	rand.Seed(time.Now().UnixNano())
}

func randomFormat() string {
	formats := []string{
		"嘿, %v. 欢迎!",
		"见到你真棒, %v!",
		"哟, %v! 很稳!",
	}

	return formats[rand.Intn(len(formats))]
}
```

### 给多个人返回招呼语

我们会在一个请求中添加对多人打招呼的功能。换句话来说，我们会处理一个多值的输入，然后用多值输出来与输入的值匹配。为了做到这点，我们需要给一个返回招呼语的函数传递一个集合的名字，这样该函数就可以给每一个人发送招呼语。

* 首先在 greetings.go 中编写一个名为 Heys 的函数，它的参数是带有多个名字的 slice。另，将其返回的类型标注为一个映射(map)，这样你便可以返回映射成招呼语的名字。

* 在函数主体中，创建一个名为 `messages` 的映射，它会将每一个接收到的名字(作为键)与一个生成的信息(作为 值)联系起来。在 Go 这门语言中，初始化一个映射的句法是这样：`make(map[key-type]value-type)`。我们会让 Heys 函数把这个映射返回给调用函数(Hey.go 中的 main)。

* 循环你的函数所接收到的名字，检查每一个名字是否不为空，然后将信息和它们联系起来。在这个 for 循环中，`range` 返回两个值：循环当前元素的索引(index)和该元素的复制值。我们并不需要索引，所以使用下划线(underscore)作为空格识别器来将其略过。

```golang
func Heys(names []string) (map[string]string, error) {
	// 将名字与信息联系起来的映射
	messages := make(map[string]string)

	// 循环名字的 slice，对每一个名字调用 Hey 函数
	for _, name := range names {
		message, err := Hey(name)
		if err != nil {
			return nil, err
		}
		messages[name] = message
	}
	return messages, nil
}
```

在 hey.go 文件中，做出下列修改：

```go
	names := []string{
		"荷马",
		"曾子",
		"庄生",
		"苏格拉底",
	}

	message, err := greetings.Heys(names)
```

输入 `go run .` 即可获得带有每个名字及其随机信息的映射。

### 添加测试

现在让我们用内置的 Go 特性来为之前的代码创建单元测试。在开发过程中测试代码可以在每当做改动时暴露 bugs。我们会为 Hey 函数添加测试。

在 greetings 目录下，创建一个名为 greetings_test.go 的文件。以 `_test.go` 结尾的文件可以让 `go test` 命令知道这个文件包含了测试函数。

* 在同一个包里编写测试函数(包声明都是 `package greetings`)

* 针对 `greetings.Hey` 创建两个测试函数，测试函数的名称需要有这样的形式：TestName，Name 指明测试的对象。另，测试函数接受一个指向测试包的 testing.T 类型的指针，作为其参数。我们使用这个参数的方法来进行测试报告以及记录。

* TestHeyName 调用 Hey 函数，传递一个 name 值(该函数应返回一个有效的响应信息)。如果调用的时候返回了一个故障，或者一个不是预期的响应信息(没有包含你传递进去的名字)，那么我们使用 t 参数的 Fatalf 方法来打印出信息，并且结束程序的执行。

* TestHelloEmpty 以一个空字符串调用 Hey 函数。这个测试是为了确认我们有妥当的故障处理。

```golang
package greetings 

import (
	"testing"
	"regexp"
)

// TestHeyName 以一个 name 调用 greetings.Hey 函数
// 检查返回的值是否有效
func TestHeyName(t *testing.T) {
	name := "Homer"
	want := regexp.MustCompile(`\b` + name + `\b`)
	msg, err := Hey("Homer")
	if !want.MatchString(msg) || err != nil {
		t.Fatalf(`Hey("Homer") = %q, %v, want match for %#q, nil`, msg, err, want)
	}
}

// TestHeyEmpty 以一个空字符串调用 greetings.Hey
// 检查是否会出故障
func TestingHeyEmpty(t *testing.T) {
	msg, err := Hey("")
	if msg != "" || err == nil {
		t.Fatalf(`Hey("") = %q, %v, want "", error`, msg, err)
	}
}

```

我们使用 `go test` 命令执行存在于测试文件(名字以 _test.go 结尾的文件)中的测试函数(函数名以 Test 开头的函数)。

### Go 的变量以及数据类型

在 Go 这门语言中，值(value) 可以分为 未命名值(unnamed value) 和 命名值(named value)。未命名值包含字面(literal)，比如说 `1945`，`"literal"` 这样的值 —— 即没有名字的数字或字符串。命名值则包括常数(constant) 和变量(variable)。

常数的值在程序运行时无法更改，以 `const` 标记。

变量的值在程序运行时可以更改，以 `var` 标记。

```go
const overtime bool = 1
const weekend int = 0
const Pi float32 = 3.1415926
var burnoutRate float32 = 1.2
```

常数和变量的命名传统都是 camelCase。

编程语言所需要处理的数据被存于计算机的内存中，以二进制数字的形式(0 和 1)。数据类型是编程语言用来表述信息的方式。Go 语言有一些基本类型，也就是它内置的数据类型。

针对数字而言，Go 有 15 种数字类型，它们被分入三个大类：

* 整数 int，比如 2021

* 浮点数 float，比如 3.1415926

* 复数 complex，比如 5 + 2i

其中整数类型有十一种，浮点数类型两种，复数类型有两种，细分的标准在于每种类型的数据需要多少位(二进制数)来表示。位数少的类型其可能存有的值也会少，同时也意味着需要存入更少的数据，也就是说会用到更少的计算机内存资源。

整数类型再被细分为 有符号整数(signed) 和 无符号整数(unsigned)。有符号整数可以是负数，但无符号整数只能是正数。这意味着一个无符号整数的最小值总是 0。由于无符号整数没有负值的可能，一个无符号整数的最大值远超同样位数的有符号整数的最大值。

Go 语言的布尔类型也是用数字表达，只需一位来储存一个布尔值，0 表示 false，1 表示 true。

下表是一些用数字表达的常见数据类型：

数据类型 | 内存用量(位数) | 最小值 | 最大值
------ | ------ | ------ | ------
int8 | 8(1字节) | -128 | 127
int16 | 16 | -32,768 | 32,767
int32 | 32 | -2,147,483,648 | 2,147,483,647
uint8 | 8 | 0 | 255
uint16 | 16 | 0 | 65,535
bool | 1 | 0 | 1

有符号整数的范围计算：最小值 = - 2<sup>(内存用量 - 1)</sup>，最大值 = 2 <sup>(内存用量 - 1)</sup> - 1

无符号整数的范围计算：最小值 = 0，最大值 = 2 <sup>(内存用量)</sup>

在我们给变量赋值之前，它们就已经有默认的初始值了。所有的数字变量在赋值之前的值为 0。字符串变量的默认初始值为 ""，也就是空字符串。布尔变量的在赋值之前的值为 false。

对于字符串类型的值，它们需要被双引号括起来。

Go 支持在同一行进行多重变量声明，以如下代码为例：

```golang
var section1, section2, section3 string
section1 = "天命之谓性"
section2 = "率性之谓道"
section3 = "修道之谓教"
```

也可以使用 := 运算符来让 Go 通过运算符右边的值来推断变量的类型：

```golang
quote, ancientClassics := "不备不虞，不可以师", true
```

### 控制流

If, else if, else 语句的写法：

```go
if 条件1 {
    操作1
} else if 条件2 {
    操作2
} else {
    操作3
}
```

逻辑运算符：

运算符 | 含义
------ | ------
&& | 与(AND)
\|\| | 或(OR)
! | 非(NOT)

Switch 语句的写法：

```go
todaysWeather := "rainy"

switch weatherRecord {
    case "sunny":
        fmt.Println("闲云潭影日悠悠，物换星移几度秋")
    case "cloudy":
        fmt.Println("溪云初起日沉阁，山雨欲来风满楼")
    case "windy":
        fmt.Println("林花谢了春红，太匆匆。无奈朝来寒雨，晚来风")
    case "rainy":
        fmt.Println("雨打梨花深闭门，忘了青春，误了青春")
    case "":
        fmt.Println("渺万里层云，千山暮雪，只影向谁去？")
    default:
        fmt.Println("试问卷帘人，却道海棠依旧")
}
```

### 随机变化

在 Go 的标准库中，这个名为 `math/rand` 的库可以帮助我们生成随机的整数。

`rand.Intn()` 这个方法中，括号中应填的是最大值，如 `fmt.Println(rand.Intn(100))` 返回的是介于 0 和 100 之间的数(包含100)。

在生成随机数的情况下，Go 会播种(seed)一个数字作为生成随机数的起点。默认情况下，这个播种值为 1。理论上来说，我们可以使用 `rand.Seed()` 方法提供一个新的播种值，然而若我们提供的仍是一个常数，那么程序在运行时所产生的随机值都是一样的。这就好比在用 Python 写机器学习的时候代码时，我们想要将数据按比例随机地分散成训练集和测试集，为了维持每次随机分组的结果不变，我们则定义 Sci-kit Learn 的 train_test_split 方法中的 random_state 参数，如下所示：

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X_normalized, y, test_size=0.2, random_state=2020)
```

然而，有的时候我们想在每一次程序运行时都生成不同的数，那么我们就需要一个变化的值作为播种值。一个普遍的做法是使用时间，因为在我们每次运行程序时，当下的时间都是不同的。

```go
package main 

import (
  "fmt"
  "math/rand"
  "time"
)
 
func main() {
  rand.Seed(time.Now().UnixNano())
  fmt.Println(rand.Intn(100))
}
```

在上述示例中，我们导入了 time 库，其中被串联的 Now() 和 UnixNano() 方法返回当下时间与 1970 年的时间差，然后这个数会被传递至 rand.Seed() 方法，从而让我们在每一次运行 rand.Intn(100) 的时候都得到一个 0 至 100 之间不同的数。

### 指针与地址

Go 是一门以值传递的语言，换言之，在给函数传递参数时，我们是将其值传入。当我们以一个参数调用函数时，Go 的编译器严格使用该参数的值，而不是该参数本身。由于这个特性，在函数中发生的改变不会影响原来的参数。

然而，通过地址(addresss)、指针(pointers)、dereferencing(消引)的方式，我们仍可以对不同的作用域的值进行修改。

```go
package main

import (
    "fmt"
    "time"
    "math/rand"
)

func timesTen(num int) {
    num *= 10
}

func main() {
    rand.Seed(time.Now().unixNano())
    aNum := rand.Intn(10)
    fmt.Println("Initial value:", aNum)
    timesTen(aNum)
    fmt.Print("Final value:", aNum)
}
```

计算机内存分配给值的存储空间被称为地址。每一个地址由一个独一无二的数值标记(通常为十六进制形式)。每次我们使用变量时，都会获取储存在该变量的地址的值。我们可以用 `&` 运算符访问一个变量的地址。

```golang

aVariable := "To find address"
fmt.Println(&aVariable)

```

指针是专门用于储存地址的变量。以 `*` 标记：

```golang

var pointerForString *string

weather := "breezy"

pointerForString = &weather

fmt.Println(pointerForString)

```

当我们想改变一个地址对应的变量的值的时候，我们可以使用指针来访问那个地址，并更改其值，这被称为消引(dereferencing)。

```golang
weather := "drizzling"

pointerForString := &weather

*pointerForString = "thunderstorm"

fmt.Println(weather)

```

回到之前将参数乘以 10 的示例，这回我们不再向 timesTen 函数递入变量的值，而是递入变量的地址，使得其值在不同的作用域中也可以发生变化，并且该变化直接作用于地址上，所以会被保留。

```go
func timesTen(num *int) {
    *num *= 10
}

func main() {
    rand.Seed(time.Now().unixNano())
    aNum := rand.Intn(10)
    fmt.Println("Initial value:", aNum)
    timesTen(&aNum)
    fmt.Print("Final value:", aNum)
}
```
