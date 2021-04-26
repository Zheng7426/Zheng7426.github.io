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

### 使用 Express  

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

位于 `app.get()` 之内的 `res` 对象拥有一个 `status()` 方法，我们可以用该方法设定 http 状态码。你可以根据这个方法来自定义报错信息：

```js
else {
    res.status(404).send('Book not found');
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
