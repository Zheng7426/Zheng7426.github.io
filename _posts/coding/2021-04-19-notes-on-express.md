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

安装 nodemon 之后，修改 package.json 中的启动脚本，便可以不必刷新就获取改动代码之后的效果：

`DEBUG=express-locallibrary-tutorial:* npm run devstart`

### 响应方法

下列表格中针对 response(res) 对象的方法可以向客户(浏览器或本地Js环境)发送响应，并且终止 请求 - 响应 周期。

方法 | 用途
------ | ------
res.render() | 渲染显示模版(view template)
res.redirect() | 重定向一个请求
res.json() | 发送一个 JSON 响应
res.end() | 结束响应过程
res.download() | 弹出一个可供下载的文件
res.send() | 发送一个可属各种类型的响应

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

模型文件通常位于 root 目录的 models 文件夹内，它们用于定义信息的结构，该结构与数据库中的 collections 对象的内容是一致的。为了从模型获取信息，路由首先会将来自用户(浏览器或移动终端)的请求发送至控制器函数。控制器函数会执行相应的数据库行动，包含从模型中读取数据，然后生成并返回网页页面。

### 网页表单

通常情况下，处理表单的代码是用 GET 路由来显示表单，然后用一个 POST 路由来对用户输入的数据进行核验、表单数据的处理。我们可以使用 express-validator 模块来对输入数据进行处理(核验和清洁)。

`npm install express-validator`

比方说我们现在想要创建让用户添加新书的表单，那么定义路由的代码如下所示：

```js
const router = express.Router();
const book_controller = require('../controllers/bookController');
router.get('/book/create', book_controller.book_create_get);
router.post('/book/create', book_controller.book_create_post);
```

在控制器文件中相应的代码如下：

```js
exports.book_create_get = function(req, res, next) {
    res.render('book_form', { title: 'Create Book' });
};

exports.book_create_post = [
    // 将书类转化成数组
    (req, res, next) => {
        if (!(req.body.genre instanceof Array)) {
            if (typeof req.body.genre === 'undefined') {
                req.body.genre = [];
            }
            else {
                req.body.genre = new Array(req.body.genre);
            }
        }
        next();
    },

    // 核验及清洁表单栏
    body('title', 'Title must be specified.').trim().isLength({ min: 1 }).escape(),
    body('author', 'Author must be specified.').trim().isLength({ min: 1 }).escape(),
    body('summary', 'Summary must be specified.').trim().isLength({ min: 1 }).escape(),
    body('isbn', 'ISBN must be specified').trim().isLength({ min: 1 }).escape(),
    body('genre.*').escape(),
    
    // 处理请求
    (req, res, next) => {
        // 从请求中提取核验过后产生的错误
        const errors = validationResult(req);

        // 创建一个数据预处理之后的 Book 对象
        const book = new Book({
            title: req.body.title,
            author: req.body.author,
            summary: req.body.summary,
            isbn: req.body.isbn.
            genre: req.body.genre
        });

        if(!errors.isEmpty()) {
            // 如果有错误的话，返回用户现已输入的信息
            async.parallel({
                authors: function(callback) {
                    Author.find(callback);
                },
                genres: function(callback) {
                    Genre.find(callback);
                }
            }, function(err, results) {
                if (err) { return next(err); }
                for (let i = 0; i < results.genres.length; i++) {
                    if (book.genre.indexOf(results.genres[i]._id) > -1) {
                        results.genres[i].checked = 'true';
                    }
                }
                res.render('book_form', { title: 'Create Book', authors: results.authors, genres: results.genres, book: book, errors: errors.array() });
            });
            return;
        }
        else {
            book.save(function (err) {
                if (err) { return next(err); }
                res.redirect(book.url);
            });
        }
    }
];
```

### 从开发环境部署至生产环境

到目前为止，我们只是在本地开发环境中写代码，并将 Express 作为网页服务器在本地的浏览器上搭建网页。在本地运行网站的同时，开发设置会暴露一些私人的信息以及修改代码的过程。那么，如何在本地环境之外搭载一个网站？

* 选择一个搭载 Express 应用的环境

* 对项目设置做出一些修改

* 给网站搭建一个生产级别的基础设施

当你用于外部访问的网站运行在一个服务器计算机上的时候，由该服务器提供的环境便称为生产环境。该环境包含以下元素：

* 网站运行所依靠的计算机硬件

* 操作系统(比如 Linux 或 Windows)

* 你的网站所基于的编程语言以及框架、库

* 网页服务器基础设施，比如说网页服务器、反向代理、负重平衡器等等。

* 你的网页所依赖的数据库

服务器计算机可以是在你触手可及的地方，也可以是 “云上” 的远程服务器或虚拟主机。远程服务器的供应商(如阿里云、腾讯云等)通常会有偿提供一些运算资源(中央处理器、内存、存储空间等)。

这样可供远程访问的运算或网络硬件被称为 “基础设施作为服务(IaaS)”。很多 IaaS 供应商会提供某些操作系统的预安装选项，然后你在操作系统中安装你生产环境所需的组件。

还有的公司对 Express 纳入它们 “平台作为服务(PaaS)” 的一部分。当使用这种搭载网站的方式时，你基本不用担心生产环境(服务器、负载平衡器等等)，因为这些平台会帮你处理这些问题。这大大简化了部署的过程，因为你只需专注于网页应用，而不是服务器的基础设施。

### 安装常用的依赖以及部署到 Heroku  

网页服务器通常可以对传回客户端的响应进行压缩，从而大幅减少客户端(如浏览器)获取以及加载页面所需的时间。

你可以为你的网站加入下列压缩中间件：

`npm install compression`

打开 ./app.js 文件，导入这个方才安装的库：

`const compression = require('compression');`

在你定义所有的路由之前，将其纳入中间件的链：

`app.use(compression());`

值得注意的是，如果你的网站流量巨大，那通常不需要用这个中间件，而你可能会需要像 nginx 那样的反向代理。

为了保护你的应用免受常见的网页漏洞(如跨域Js注射)，我们可以使用名为 Helmet 的中间件库，它可以帮助我们设置适当的 HTTP 头文件。

`npm install helmet`

打开 ./app.js 文件，导入这个方才安装的库：

```js
const helmet = require('helmet');
app.use(helmet());
```

接下来我们要往 Heroku PaaS 云平台安装我们的 LocalLibray 应用。Heroku 是流行已久的的基于云的 PaaS 服务商。

Heroku 在一个或多个 "Dynos" 中运行网站。这些 "Dynos" 是封闭的虚拟化 Unix 容器，这些容器提供了运行应用所需的环境。它们的文件系统是临时的(每次重启时都会被清空)。默认情况下，所有 Dynos 都有应用的配置变量。

为了执行你的应用，Heroku 需要被配置合适的环境，以应对你的应用的依赖。对于 Node 应用来说，Heroku 所需的信息都可以从 package.json 文件中获取。

你可以使用一个特殊的、类似于 Unix bash 脚本的客户端应用或终端来与 Heroku 进行交互。该终端允许你上传贮存于 git 仓库的代码、查看运行中的进程、日志、设置配置变量等等。

Heroku 自带 git —— 十分流行的源代码版本控制系统，我们安装了 Heroku 客户端之后，它会使用 git 来同步你上传的改动。Heroku 客户端会创建一个新的名为 heroku 的 “远程” (其实是本地)仓库。这个 heroku 会与你部署在 Heroku 云上的代码仓库连接。在开发过程中，你使用 git 在本地的仓库存储改动，当你要部署你的网站时，便将本地的改动同步至 Heroku 仓库。

为了使我们的应用可以在 Heroku 上正常使用，我们首先要对 package.json 文件做出修改。

添加 Node 版本：

```json
  "name": "locallibrarytutorial",
  "version": "0.0.0",
  "engines": {
    "node": "14.15.3"
  },
```

通常情况下，在生产环境的数据库和在开发环境的数据库应该是不同的。在 app.js 文件中，MongoDB 连接变量的定义如下：

```js
const mongoDB = 'mongodb+srv://用户名:密码@cluster0.mb6wf.mongodb.net/local_library?retryWrites=true&w=majority';
```

将其修改为如下代码：

```js
const dev_db_url = 'mongodb+srv://用户名:密码@cluster0.mb6wf.mongodb.net/local_library?retryWrites=true&w=majority';
const mongoDB = process.env.MONGODB_URI || dev_db_url;
```

在 heroku 的官网上下载其客户端之后，在本地 CLI(控制命令行接口) 输入 `heroku login` 进行登录。进行网页登录之后，回到 CLI，输入以下代码：

`heroku create`

这将会在我们本地 git 环境中创建一个指向远程 git 仓库的名为 heroku 的指针。
This creates a git remote ("pointer to a remote repository") named heroku in our local git environment.

输入 `git push heroku main` 会将我们的应用推送至远端的 Heroku 仓库。然后输入 `heroku open` 就可以打开刚刚上传的网页了。

要想区分开发环境和生产环境的数据库，在 CLI 进行操作，设置配置变量的代码如下：

`heroku config:set NODE_ENV='production'`

`heroku config:set MONGODB_URI=mongodb+srv://新用户名:密码@cluster0.ajr9j.mongodb.net/myFirstDatabase?retryWrites=true&w=majority`

使用 `heroku config` 查看配置是否已经被改动。若要查看正在运行的应用的信息，可以使用以下代码：

`heroku logs --tail`

若想查看 Dyno 的状态，使用 `heroku ps`(类似 Docker)。
