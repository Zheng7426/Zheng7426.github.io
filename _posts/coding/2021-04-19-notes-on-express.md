---
layout: post
title: "Express.js笔记"
date: 2021-04-19 00:00:00 -0000
categories: coding 
---

Express 是一个用于创建网络服务器和 API 接口的框架(framework)。

### CRUD  

CRUD 是常用的 API 所要达到的四种功能。

* Create 创建

* Read 读取

* Update 变更

* Delete 删除  

### 下载与使用 Express  

使用 Express 的前提是安装 node.js 以及其包裹管理器 npm。以下命令可以检验它们是否已经被安装于你的环境中：

`node --version`

`npm --version`

确保满足前提要求之后，可以新建文件夹，并且进行初始化(创建 package.json 以追踪该项目已安装哪些依赖):

`mkdir app`
`cd app`
`npm init`

然后安装 express：

`npm install express`

建立一个名为 newApp.js 的文件，在其中导入 Express 模块：

```js
const express = require('express');
```  

将 Express 的一个实例赋予 `app` 这个常数：

```js
const app = express();
```

在“请求--响应”模型中，服务器的作用是聆听由客户(如浏览器)发出的请求，对请求进行响应操作，然后返回响应。因此，我们需要标注让服务器聆听哪个端口，以接收发来的请求。

```js
// process.env.PORT 是当前进程环境的默认端口
const portNumber = process.env.PORT || 4001;
app.listen(portNumber, () => {
    console.log(`服务器正在聆听 ${portNumber} 端口`);
});
```

开启服务器：

```
node newApp.js
```

在诸多请求类型中，GET 请求用于从服务器获取资源。想要注册能够匹配 GET 请求的路由，可以使用 Express 的 `app.get()` 方法。Express 路由通常接受两个参数：一个路径(格式为**服务器地址:端口/api路径**)以及负责处理请求并发送响应的回调函数(处理器)。

一个路由(route)是一段将 HTTP 动词，一个 URL 样式，以及一个处理该样式的函数联系而成的 Express 代码。

路由函数是 Express 中间件(middleware)，也就是说它们必须完成(发出响应)请求或者调用中间件链的下一个(next)函数。

Express 服务器使用响应对象的 `.send()` 方法来发送响应。

```js
const books = [{ book: 'The Shadow of the Wind'}, { book: 'Identity' }];
app.get('/books', (req, res, next) => {
  res.send(books);
});
```

路由(Routes)被注册的**顺序**是有影响的，Express 会按顺序对路由的代码进行搜索，第一个匹配到的路由会被采用，且它的回调函数会被调用。

路由参数是路由路径中以 `:` 开头的部分，比如说 `books/:id` 可以同时匹配 `books/1` 和 `books/70`，所以参数可以用于动态的路径。

```js
const books = { 'Mere Christianity': { author: 'C.S.Lewis', year: 1952 }, 'The Lord of the Ring': { author: 'J.R.R. Tolkien', year: 1949 } };
// GET /books/mere-christianity
app.get('/books/:name', (req, res, next) => {
  console.log(req.params) 
  res.send(books[req.params.name]);
});
```

Express 会对参数解析，并提取参数所指向的实际的值，然后将它们放入 request 对象内嵌的名为 `req.params` 对象。

比如在 `http://localhost:3000/users/7/books/45` 这个 URL 中，我们可以这样提取其中的信息：

```javascript
app.get('/users/:userId/books/:bookId', (req,res) => {
  // 可通过 req.params.userId 访问 userId
  // 可通过 req.params.bookId 访问 bookId
  res.send(req.params);
})
```

位于 `app.get()` 之内的 `res` 对象拥有一个 `status()` 方法，我们可以用该方法设定 http 状态码。你可以根据这个方法来自定义报错信息：

```js
else {
    res.status(404).send('Book not found');
}
```  

或者新建一个 Error 的实例：

```js
if (results.book === null) {
  const err = new Error('Book not found');
  err.status = 404;
  return next(err);
}
```

### 其他 HTTP 协议的方法动词

HTTP 动词 | Express 方法
------ | ------
GET   | app.get()
POST | app.post()
PUT | app.put()
DELETE | app.delete()

PUT 请求用来更新已存在的资源，比如说更新书的出版年份。POST 请求用于创建新资源，而 DELETE 请求则用于删除已存在的资源。

**查询字符串(Query String)** 可以在发送请求时附加信息，它们出现在网址路径的最后，以问号为标记。查询字符串并不属于路由路径的一部分，Express 服务器会将其解析成一个附着在请求上的 JavaScript 对象 —— `req.query`。例如，在查询书籍的时候，在 /books/1?name=Identity&year=2016 中, 路径是 /books/1/，查询字符串是name=Identity&year=2016。

使用 POST 请求时，路径的结尾不会有路径参数，因为新的资源还未生成。对于刚被成功创建的资源，对应的 HTTP 响应状态码为 201。

### 应用生成器

你可以使用应用生成器来快速地为一个项目构建其骨架代码。安装 express-generator 的步骤如下：
`npm install express-generator -g`

### 数据库

Express 应用可使用 Node 所支持的任何数据库，常见的选择包括这些：

* MongoDB
* PostgreSQL
* MySQL
* Redis

通常情况下，与数据库进行交互有两种途径：

1. 使用数据库的原生查询语言
2. 使用对象数据模型(Object Data Model)，ODM 将网站的数据以 JavaScript 对象的形式保存，然后再映射给具体的数据库。使用对象数据模型通常比使用原生查询语言要慢。

[Mongoose](https://www.npmjs.com/package/mongoose) 是一个适用于异步环境的 MongoDB 的对象模型工具。MongoDB 是一个使用面向文档数据模型的开源 NoSQL 数据库。MongoDB 中的 collection 对应关系型数据库(如 MySQL) 中的 table，而 documents 对应 rows。


### 开发范式：模型(Model) - 显示(View) - 控制器(Controller)

模型文件通常位于 root 目录的 models 文件夹内，它们用于定义信息的结构，该结构与数据库中的 documents 对象的内容是一致的。为了从模型获取信息，路由首先会将来自用户(浏览器或移动终端)的请求发送至控制器函数。控制器函数会执行相应的数据库行动，包含从模型中读取数据，然后生成并返回网页页面。

### 网页表单

通常情况下，处理表单的代码是用 GET 路由来显示表单，然后用一个 POST 路由来对用户输入的数据进行核验、表单数据的处理。我们可以使用 express-validator 模块来对输入数据进行处理(核验和清洁)。

`npm install express-validator`


