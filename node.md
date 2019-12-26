# node
## node内置模块
### 1.fs
- 读文件 fs.readFile
```js
var fs = require('fs')

// 异步读文件
fs.readFile('sample.txt', 'utf-8', function(err, data){
  if(err){
    console.log(err)
  } else 
  console.log(data)
})

// 同步读文件
try {
  var data = fs.readFileSync('sample.txt', 'utf-8')
  console.log(data)
}
catch(err) {
  console.log(err)
}
```
- 写文件 fs.write
writeFile()的参数依次为文件名、数据和回调函数。如果传入的数据是String，默认按UTF-8编码写入文本文件，如果传入的参数是Buffer，则写入的是二进制文件。回调函数由于只关心成功与否，因此只需要一个err参数。
```js
/* 异步 */
var data = 'hello node.js'
fs.writeFile('out.txt', data, function (err) {
  if (err) {
    console.log(err)
  } else console.log('ok')
})

/* 同步 */
fs.writeFileSync('output.txt', data)
```
- 获取文件信息通过fs.stat()，它返回一个Stat对象
stat.isFile() stat.isDirectory() stat.size stat.birthtime stat.mtime

### 2.stream
```js
var rs = fs.createReadStream('sample.txt', 'utf-8')

rs.on('data', function (chunk) {
    console.log('DATA:')
    console.log(chunk)
})

rs.on('end', function () {
    console.log('END')
})

rs.on('error', function (err) {
    console.log('ERROR: ' + err)
});
```

### 3.http
request对象封装了HTTP请求，我们调用request对象的属性和方法就可以拿到所有HTTP请求的信息；
response对象封装了HTTP响应，我们操作response对象的方法，就可以把HTTP响应返回给浏览器。
- 一个简单的http服务示例
```js
// 导入http模块:
var http = require('http')
// 创建http server，并传入回调函数:
var server = http.createServer(function (request, response) {
    // 回调函数接收request和response对象,
    // 获得HTTP请求的method和url:
    console.log(request.method + ': ' + request.url)
    // 将HTTP响应200写入response, 同时设置Content-Type: text/html:
    response.writeHead(200, {'Content-Type': 'text/html'})
    // 将HTTP响应的HTML内容写入response:
    response.end('<h1>Hello world!</h1>')
})

// 让服务器监听8080端口:
server.listen(8080)
console.log('Server is running at http://127.0.0.1:8080/')
```
- 文件服务器
  - url模块
`url.parse('http://user:pass@host.com:8080/path/to/file?query=string#hash')`
  - path模块
```js
// 解析当前路径
var workDir = path.resolve('.')
// 组合完整的文件路径:当前目录+'pub'+'index.html':
var filePath = path.join(workDir, 'pub', 'index.html')
var filePath = path.join(__dirname, 'index.html')
```
文件服务器
```js
'use strict';

var
    fs = require('fs'),
    url = require('url'),
    path = require('path'),
    http = require('http');

// 从命令行参数获取root目录，默认是当前目录:
var root = path.resolve(process.argv[2] || '.');

console.log('Static root dir: ' + root);

// 创建服务器:
var server = http.createServer(function (request, response) {
    // 获得URL的path，类似 '/css/bootstrap.css':
    var pathname = url.parse(request.url).pathname;
    // 获得对应的本地文件路径，类似 '/srv/www/css/bootstrap.css':
    var filepath = path.join(root, pathname);
    // 获取文件状态:
    fs.stat(filepath, function (err, stats) {
        if (!err && stats.isFile()) {
            // 没有出错并且文件存在:
            console.log('200 ' + request.url);
            // 发送200响应:
            response.writeHead(200);
            // 将文件流导向response:
            fs.createReadStream(filepath).pipe(response);
        } else {
            // 出错了或者文件不存在:
            console.log('404 ' + request.url);
            // 发送404响应:
            response.writeHead(404);
            response.end('404 Not Found');
        }
    });
});

server.listen(8080);

console.log('Server is running at http://127.0.0.1:8080/');
```
### 4.crypto
crypto模块的目的是为了提供通用的加密和哈希算法。


&emsp;
&emsp;
***
&emsp;
&emsp;


## express
安装：npm i express --save
下面几个模块可选：
npm install body-parser --save // node.js 中间件，可用于post请求解析body
npm install cookie-parser --save // 解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象
npm install multer --save //  node.js 中间件，用于处理 enctype="multipart/form-data"的表单数据
```js
const express = require('express')
const app = new express()
app.get('/', function (req, res) {
  res.send('hello world')
})
app.listen(3000, () => console.log('app is starting in port 3000...'))
```



&emsp;
&emsp;
***
&emsp;
&emsp;
## koa2
### 1.创建http服务
```js
// npm i koa
const Koa = require('koa')
const app = new Koa()

app.use(async (ctx, next) => {
  await next()
  ctx.response.type = 'text/html'
  ctx.response.body = '<h1>hello world</h1>'
})

app.listen(3000)
console.log('server is running port 3000...')
```
### 2.使用koa的路由中间件
`npm i koa-router`
```js
const Koa = require('koa')
const router = require('koa-router')()  // 这里不要写错
const app = new Koa()
app.use(router.routes()) // 注册路由模块

router.get('/hello/:name', async (ctx, next) => {
  ctx.response.body = `<h1>hello, ${ctx.params.name}</h1>`
})

app.listen(3000)
console.log('server is running in port 3000...')
```
用post请求处理URL时，我们会遇到一个问题：post请求通常会发送一个表单，或者JSON，它作为request的body发送，但无论是Node.js提供的原始request对象，还是koa提供的request对象，都不提供解析request的body的功能！所以要用到koa-bodyparser中间件

### 3.使用koa解析request的中间件koa-bodyparser
- koa-bodyparser必须在koa-router之前注册到app上
```js
const Koa = require('koa')
const router = require('koa-router')()
const bodyParser = require('koa-bodyparser')
const app = new Koa()
app.use(bodyParser())
app.use(router.routes()) // 注册路由模块

router.get('/', async (ctx, next) => {
  ctx.response.body = `<h1>Index</h1>
      <form action="/signin" method="post">
          <p>Name: <input name="name" value="koa"></p>
          <p>Password: <input name="password" type="password"></p>
          <p><input type="submit" value="Submit"></p>
      </form>`
})

router.post('/signin', async (ctx, next) => {
  var
      name = ctx.request.body.name || '',
      password = ctx.request.body.password || ''
  if (name === 'koa' && password === '12345') {
      ctx.response.body = `<h1>Welcome, ${name}!</h1>`
  } else {
      ctx.response.body = `<h1>Login failed!</h1>
      <p><a href="/">Try again</a></p>`
  }
})

app.listen(3000)
console.log('start')
```
