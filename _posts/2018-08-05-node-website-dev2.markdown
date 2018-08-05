---
layout: post
title: 使用Node开发网站 中级篇
date: 2018-08-05 15:50:24.000000000 +09:00
tag: nodejs, tech
---

### 写在学习之前
学完基础的node知识以后，通过实践来进一步的加深对nodejs的理解
加深对一个东西的理解，最好的方法就是动手去做一个真实的项目，踩过很多坑之后，才算是对一个东西的真正掌握。

### 进击的Nodejs
nodejs也好，javascript也好，之所以可以火起来的原因，个人认为是因为有了插件这个概念。自己在上大学的时候，也学习过javascript的东西，但是当时只是一个脚本语言，并没有太强大的功能，这次重新学习之后，发现本质上其实是一样的，但是一些很漂亮的效果都是通过插件这种形式，使得JS变得非常强大。包括自己现在在用的ATOM这个编辑器一样，虽然核心的功能就是一个编辑器，但是通过不断的安装各种package，当然这也是一个插件的概念，使得这个编辑器几乎变成了一个万能的东西，任何语言，任何脚本，都可以在这个核心的基础上来得到增加，更多的插件，更强大的功能。这或许可以给自己提供一个新的思路。

常见的web服务框架 Sail, Express, Hapi


# Koa2 实现微信公众号前后端开发
课程内容 开发一个可以实时更新的预告片网站
未来给自己的作业，开发一个可以自动更新的奇奇的图片和视频的网站，算是给孩子的礼物

Koa2 + MongoDB + Mongoose + Pug + Bootstrap + 微信 JS-SDK
同时学习Nodejs，MongoDB，Puppeteer，AntDesign，Bootstrap和Parcel

需要这套视频教程的朋友，请联系我

```
Koa2是Nodejs的上层Web框架
第1章 2018 年的编程姿势
第2章 必会 ES6-7 语法特性与规范
第3章 层层学习 Koa 框架的
第4章 Koa2 与 Koa1 、Express 框架对比
第5章 从 0 开发一个电影预告片网站
第6章 利用爬虫搞定网站基础数据
第7章 彩蛋篇 - [高难度拔高干货] 深度理解 Node.js 异步 IO 模型
第8章 实战篇 - 在 Koa 中向 MongoDB 建立数据模型
第10章 实战篇 - 集成 AntDesign 与 Parcel 打通前后端与构建
第11章 实战篇 - 实现网站前端路由与页面功能
第12章 实战篇 - 实现后台登录权限与管理功能
第13章 服务器部署与发布
第14章 课程总结与展望
```
```
自己之前做的是操作层面的东西，不过对于前端的技术也很感兴趣，现在趁着有时间，要把前后端整个打通，为以后做好准备。
```
### 学习笔记

nodejs的下载
* 更新到最新的长期支持版本,保持跟进

#### 安装
```
nvm ls
nvm install v8.9.2
nvm use v8.9.2
nvm alias default v8.9.2
node -v
```
Promises
一个规范，提供Promises接口
在框架中有大规模的使用

cd-promise.js
```
const fs = require(fs)
//回调
fs.readFile('./package.json',(err,data) => {
  if(err) return console.log(err)
  data = JSON.parse(data)

  console.log(data.name)
  })
```


cd-promise2.js
```
const fs = require('fs')
const Promise = require('bluebird')

function readFileAsync (path) {
  return new  Promise((resolve,reject) => {
    fs.readFile(path,(err,data) => {
      if(err) reject(err)
      else resolve(data)
      data = JSON.parse(data)
      console.log(data.name)
    })
    })
}

readFileAsync('./package.json')
  .then(data => {
    data = JSON.parse(data)

    console.log(data.name)
    })
    .catch(err => {
      console.log(err)
      })
```
cd-promise3.js
```
const util = require('util')
util.promisify(fs.readFile)('./package.json')
  .then(JSON.parse)
  .then(data => {
    console.log(data.name)
    })
    .catch(err => {
        console.log(err)
    })
```

```
使用封装在util里面的promise，代码简洁，减少了80%的代码量，不过感觉前段的进化速度还是有点快
```

package.json
```

```

```
npm init
```
执行程序
```
node cb-promise.js
```

使用async funciton
使用同步的代码，完成异步的操作

promise-async.js
```
const fs = require('fs')
const util = require('util')
const readAysnc = util.promisify(fs.readFile)

aysnc function init(){
  try{
    let data = await readAysnc('./package.json')
    data = JSON.parse(data)

    console.log(data.name)
  } catch (err) {
    console.log(err)
  }
}
init()

```
借助Bible支持最新的特性

迭代器

iterator.js
```
function makeIterator (arr) {
  let nextIndex = 0
  //返回一个迭代器对象
  return {
    next: () => {
      　//next()方法返回的结果对象
        if(nextIndex < arr.length)
        return {value:arr[nextIndex++],done:false
        } else {
          return {done:true}
        }
    }
  }
}

const it = makeIterator(['吃饭','睡觉','打豆豆'])

console.log('首先',it.next().value)
console.log('其次',it.next().value)
console.log('然后',it.next().value)
console.log('最后',it.next().value)
```

生成器
```
function *makeIterator (arr){
  for(let i = 0, i< arr.length. i++){
    yield arr[i]
  }
}

const gen = makeIterator(['吃饭','睡觉','打豆豆'])

console.log('首先',gen.next().value)
console.log('其次',gen.next().value)
console.log('然后',gen.next().value)
console.log('最后',gen.next().value)
```

生成器简化了迭代器构造对象的繁琐过程，同时保证了逻辑清晰

tj大神
贡献了很多高质量的框架和模块

co库
```
npm -i co
npm -i node-fetch
```
作用：把所有传入的参数都转换为promise

co.js
```
const co = require('co')
const fetch = require('node-fetch')

co(function *() {
  const res = yeild fetch('https://api.douban.com/v2/movie/1291843')
  const movie = yield res.json()
  const summary = movie.summary

  console.log('summary',summary)
  })

```
yield 实现了一个generator的自动执行


使用run函数来执行co的过程
```
const co = require('co')
const fetch = require('node-fetch')

<!-- co(function *() {
  const res = yeild fetch('https://api.douban.com/v2/movie/1291843')
  const movie = yield res.json()
  const summary = movie.summary

  console.log('summary',summary)
  }) -->

function run (generator) {
  const iterator = generator()
  const it = iterator.netxt()
  const promise = it.value

  promise.then(data => {
    const it2 = iterator.next(data)
    const promise2  =it2.value

    promise2.then(data2 => {
      iterator.next(data2)
      })
    })
}

run(function *() {
  const res = yeild fetch('https://api.douban.com/v2/movie/1291843')
  const movie = yield res.json()
  const summary = movie.summary

  console.log('summary',summary)
  })

```
co会把生成的过程自动化


箭头函数

传统函数的写法
```
function (data){

}
```
箭头函数的写法
````
data => {

}
````

error.js
```
const arrow = function (param) {}

const arrow = (param) => {}

const arrow = param => {}

const arrow = param => console.log(param)

const arrow = param = ({param: param})

const arrow = (param1, param2) => {}

const arrow = ({id, movie}) => {
    console.log(id,movie)
}

const luke = {
  id:2
  say: function(){
    setTimeout(function (){
      console.log('id:', this.id)
      },50)
  },
  sayWithThis: function (){
    let that = this //self me  _this
    setTimeout(function (){
      console.log('this id:', that.id)
      },500)
  },
  sayWithArrow: function(){
    setTimeout(() => {
      console.log('arrow id:', this.id)
      },1500)
  },
  sayWithGlobalArrow: () => {
    setTimeout(() => {
      console.log('global arrow id:', this.id)
      },2000)
  }
}

luke.say()
luke.sayWithThis()
luke.sayWithArrow()
luck.sayWithGlobalArrow()

```

异步函数
第一阶段，一般通过回调函数来实现异步函数

```
const fs = require('fs')
//const Promise = require('bluebird')

function readFile (cb) {
    fs.readFile('./package.json',(err,data) => {
      if(err) return cb(err)
      data = JSON.parse(data)
      cb && cb(null.data)
    })
}

readFile((err,data) => {
  if(!err){
    data = JSON.parse(data)
    console.log(data.name)
  }
  })
```
第二阶段.使用promise来实现
```
const fs = require('fs')
//const Promise = require('bluebird')

function readFileAsync (path) {
  return new Promise((resolve, reject) => {
    fs.readFile(path,(err,data) => {
        if(err) reject(err)
        else resolve(data)
    })
    })
}

readFileAsync(('./package.json')
  .then(data => {
    data = JSON.parse(data)
    console.log(data.name)
    })
    .catch (err => {
      console.log(err)
      })

```
第三阶段，使用co库＋Genratorfunction+ Promise来实现

```
const co = require('co')
const util = require('util')

co(function *() {
  let data = yield util.promisify(fs.readFile)('./package.json')
  data = JSON.parse(data)
  console.log(data.name)
}

)
```

//第四个阶段 Async统一世界
```
const util = require('util')
const readAsync = util.promisify(fs.readFile)

async function init () {
  let data = await readAsync('./package.json')
    data = JSON.parse(data)
    console.log(data.name)
}
init ()

```
语言在不断的进化

Async在8.0以后就可以自由使用

使用Babel使用import和export

module.js
```
const fs = require('fs')

fs.writeFile

//运行时加载
const {writeFile} = require('fs')
```

静态加载
```
nopm i babel-cli babel-preset-env
```
新增配置文件
.babelrc
```
{
  "presents": [
    [
      "env",
      {
        "targets":{
          "node":"current"
        }

      }
    ]
  ]
}

运行babel


安装nodemon
```
npm -i nodemon
```
修改配置文件package.json 
```
"dev":"nodemon -w src --exec \"babel-node src
--presents env\"",
```

```
index.js
```
import fs from 'fs'

```

```
import {writeFile} from 'fs'

```
运行
```
run dev
```

index.js
```
import {promisify} from 'util'
import {resolve as r } from 'path'
import {readFile, writeFileSync as wfs} from 'fs'

import * as qs from 'querystring'

promisify(readFile)(r(__dirname,'./package.json'))
  .then(data => {
    data = JSON.parse(data)
    console.log(data.name)
    wfs(r(__dirname,'./name'),String(data.name),'utf8')
  })

```
查看更加详细的用法
关键字 mozila mdn import export


ex.js
```
export const name = 'Luke'
export const getName = () =>{
  return name
}
```


Test.js
```
import {name} from './ex'
import {getName} from './ex'

import age from './ex'

console.log(age)
console.log(name)
console.log(getName())
```

age.js
```
const age = 19
export default age
```
export的用法
单独导出一个方法或者对象
也可以批量导出对象
import {} from ''

修改配置文件package.json
```
"build": "rimraf babel src -s -D -d dist --presents env"

```
运行编译，将ES6.7转换为可以支持的特性
```
npm i rimraf
rpm run build
```
```
import {}
```


index.js
```
const util = require('util')
const readAsync = util.promisify(fs.readFile)

async function init () {
  let data = await promisify(readFile()(r(__dirname,'./package.json'))
    data = JSON.parse(data)
    console.log(data.name)
}
init ()

```

```
npm run dev
```

```
npm run build
```

配置插件
```
npm i -S babel-plugin-transform-runtime babel-runtime
```
```
"pluginins":[
  [
    "transform-runtime",{
      "polyfill":false,
      "regenrator":true
    }
  ]
]
```



# 层层学习 Koa 框架的 API

Koa Express

接收，解析以及响应HTTP的请求
中间件

执行上下文：托管中间件

Application
Context
Request
Response
Middlewares
Seesion
Cookie

从源码的角度进行学习

安装
```
npm i koa
```

源文件
server/index.js
```
consta Koa = require ('koa')
consta app = new Koa()

app.use(async (ctx.next) => {
  ctx.body = 'Hi Luke'
})
app.listen(2333)
```
运行
```
node server/index.js
```
在浏览器中执行
```
127.0.0.1：2333
```
查看源码
koa/package.json中的main

wen服务类application
框架的使用和框架的实现原理

看框架的方法：
```
首先看ReadMe.md(十分钟)，
然后选择性的看一下History.md看迭代的历史
然后看package.json中看main找到入口文件lib/application.js
```
依赖模块
* compose中间件函数数组
* context运行服务的上下文
* request客户端请求
* statuses状态
* Cookies记录客户信息
* accepts协议和资源的控制
* Emitter事件循环 
* assert断言
Stream流
http
only
convert
deprecate接口是否过期

不要上来就盯细节
删掉if，边界条件的处理
删掉异常处理，只考虑正常情况

constructor()
数据的进request，数据的出response
继承自Emitter,在构造器中声名了一些属性

listen
  创建一个服务器实例
  然后让服务器实例去监听端口号

use
  推进中间件

callback
  调用handleRequest

handleRequest
  向客户端访问数据
  把请求的上下文对象交给中间件，然后把处理完的结果交给handlerespone

createContext

respond
  res.end向客户端返回数据


传入中间件，监听端口，生成服务器实例
拿到http实例，然后中间件处理，然后把数据返回给客户端

const app = new Koa()
app.use(middleware)
app.listen(2333)

上下文对象context
  
  就是一个对象

delegate代理，委托，将一些方法嫁接过来
创建一个实例，用来操作proto

画图工具mindnode

### Request源码
request.js
get，set：获取和修改属性值

* get
* set

console.log(ctx.href)
ctx.path
ctx.url
ctx.method
通过context拿到一些信息

### Response源码
response.js
定义了一些属性和方法
* get，set：获取和修改属性值

* socket套接字
* get header 拿到头信息
* get status 拿到服务端状态码
* set status
* ...
* vary() 验证客户端和服务端的内容
* redirect 重定向
* attachment 附件
* type 文档类型
* etag
* ...

中间件
Server.js
```js
const mid1 = async (ctx, next) => {
  ctx.type = 'text/html; charset = utf-8'
  await next()
  ctx.body = ctx.body + 'Hello'
}

const mid2 = async (ctx, next) => {
  ctx.body = 'Hi'
  await next()
}

const mid3 = async (ctx, next) => {
  ctx.body = ctx.body + 'Fan'
}
app.use(mid1)
app.use(mid2)
app.use(mid3)

app.listen(2333)

```
use里面都是中间件
中间件顺序执行
中间件执行过程中允许中断

官方中间件来验证过程
```
npm i koa-logger
```
```
const logger = require('koa-logger')
app.use(logger)
```

纯函数
函数满足对于唯一的参数输入x，一定会输出y
```
function pure (x) {
  return x + 1
}
```
尾递归
自己调用自己

compose(数组，数组中的每一项是function)
返回Promise

一个函数的输出就是另一个函数的输入，就像一个多米诺骨牌一样联动起来。

使用Seesion
```
npm i koa-seesion
```
安装session以后，可以查看源代码
服务器端和客户端的会话
```js
const session = require('koa-session')
app.Keys = ['Hi fan]
app.use(session(app))

app.use()
...
app.listen(2333)
```

路由
识别不同的页面
```js
app.use(ctx => {
  if(ctx.path === '/'){
    let n = ctx.session.views || 0
    ctx.session.views = ++n
    ctx.body = n +'Times'
  } else if(ctx.path == '/hi'){
    ctx.body = 'Hi, fan'
  } else {
    ctx.body = '404'
  }
})
```
通过path实现路由识别,制定路由规则

总结
在koa中，一切流程都是中间件
都要流经中间件
顺序执行中间件，传递控制权
每一个中间件都会拿到上下文，可以访问属性和方法
context,request,response可以互相引用

# Koa2 与 Koa1 、Express 框架对比

略过

# 从0开发一个电影网站

预告片的电影网站

后台管理页面


## 搭建一个远端的git仓库
github/douban-trailer
Username: Scott Dong

提供私有仓库
gitee.com

初始化为nodejs项目
```
npm init
```
server/inde.js
```js
const Koa = require('koa')
const app = new Koa()
app.use(async(ctx,next) =>{
  ctx.body = 'Hello Boy'
})
app.listen(4455)
```
安装最新版的koa
```
npm i koa@latest
```
配置package.json文件
```
"statrt": "node server/index.js"
```
运行
```
npm start
```

## 服务器返回一个静态HTML页面
server/tpl/normal.js
```js
module.exports = `
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Server</title>
    <link href="bootstrap" rel="stylesheet">
    <script src="bootstrap js"></script>
    <srcipt src="jquery js" ></script>
  </head>
  <body>
    <div class="container">
      <div class="row">
        <div class="col-md-8">
          <h1>Hi, Fan</h1>
          <p>This is fan</p>
        </div>
        <div class="col-md-4">
         <p>Test</p>
        </div>
      </div>
  </body>
</html>
`
```
又拍云CDN

server/inde.js
```js
const Koa = require('koa')
const app = new Koa()
const {normal} = require('./tpl')

app.use(async(ctx,next) =>{
  ctx.type = 'text/html; charset=utf-8'
  ctx.body = normal
})
app.listen(4455)
```

server/tpl/index.js
```js
const normalTpl = require('./normal')

module.exports = {
  normal:normalTpl
}
```
## 集成模板引擎koa 搭建初始模板目录
模板：快速搭建网站

server/tpl/index.js
```js
module.exports = {
  normalTpl:require('./html')
  ejsTpl:require('./ejs')
  pugTpl:require('./pug')
}
```

在github上查找ejs
server/tpl/ejs.js(拷贝client.html的内容)
```

```

```
npm i ejs
```
jade
带你学习Jade模板引擎

pug.js
```
module.exports = '
doctype html
html
  head
    meta(charset="utf-8")
    meta(name="viewport")
    title Hi,Server
    link()
    script()
    script()
  body
    .container
      .row
        .col-md-8
          h1 Hi #{you}
          p This is #{me}
        .col-md-4
          p Test Pug Page
```

server/index.js
```js
const Koa = require('koa')
const app = new Koa()
const {normal, ejsTpl, pugTpl } = require('./tpl')
const pug = require('pug')

app.use(async(ctx,next) =>{
  ctx.type = 'text/html; charset=utf-8'
  ctx.body = pug.render(pugTpl,{
    you: 'Fan',
    me: 'xin'
  })
})
app.listen(4455)
```
koa-views
template engine  

通过pug引擎，制定模板文件位置为views
模板文件的后缀名为pug
server/index.js
```js
const Koa = require('koa')
const app = new Koa()
const views = require('koa-views')
const { resolve } = require('path')

app.use(views(resolve(__dirname,'./views'),{
  extension:'pug'
}))

app.use(async(ctx,next) =>{
  await ctx.render('index',{
    you:'fan',
    me: 'xin'
  })
  })
})
app.listen(4455)
``` 
views/index.pug，实现继承关系
先拿过default的内容，然后填入block块的内容
```js
extends ./layouts/default

blcok title
  title First Page

block content
  .container
    .row
      .col-md-8
        h1 Hi #{you}
        p This is #{me}
      .col-md-4
        p Test Pug Page
```

```js
module.exports = '
doctype html
html
  head
    meta(charset="utf-8")
    meta(name="viewport")
    title Hi,Server
    link()
    script()
    script()
  body
    .container
      .row
        .col-md-8
          h1 Hi #{you}
          p This is #{me}
        .col-md-4
          p Test Pug Page
```
一个网站的几个部分
title 从外面传进来

view/layouts/default.pug
使用include包含进样式和脚本

```js
module.exports = '
doctype html
html
  head
    meta(charset="utf-8")
    meta(name="viewport")
    block title
    include ../includes/style
  body
    block content
    include ../incluede/script
```
view/includes/style.pug
```
<link href="bootstrap" rel="stylesheet">

```

view/include/script.pug
```
<script src="bootstrap js"></script>
<srcipt src="jquery js" ></script>
```

## 借助bootstrap 4-x搭建网站首页

server/index.pug
```js
extends ./layouts/default

blcok title
  title First Page

block content
  
  include ./includes/header

  .container-fluid
    .sidebar
    .content
      .row
        .col-md-6
          .card
            img.card-img-top(src='',data-video='')
            .card-body
              h4.card-title title
              p.card-desc description
            .card-footer
              small.text-muted one day ago
        .col-md-6
                  .card
            img.card-img-top(src='',data-video='')
            .card-body
              h4.card-title title
              p.card-desc description
            .card-footer
              small.text-muted one day ago
      .row
        .col-md-6
          .card
            img.card-img-top(src='',data-video='')
            .card-body
              h4.card-title title
              p.card-desc description
            .card-footer
              small.text-muted one day ago
        .col-md-6
                  .card
            img.card-img-top(src='',data-video='')
            .card-body
              h4.card-title title
              p.card-desc description
            .card-footer
              small.text-muted one day ago
弹窗组件
#myModal.modal.fade.bd-example-modal-lg()
...


include ./includes/script

script.
  var player = null;
  判断播放器是否暂停
  ${document}.ready(function(){
    $('#myModal').on('hidden.bs.modal',function(e){
      if(player && player.pause) player.pause()
    })

    $('.card-img-top').click(function (e){
      var image = $(this).data('video')
      var image = $(this).attr('src')

      $('#myModal').modal('show')

      if(!player){
        player = new DPlayer({
          container: document.getElementById('videoModal')
          screenshot: true,
          video: {
            url: video,
            pic:image
            thumbnails: image
          }
        })
      } else{
        if(play.video.currentSrc !== video){
          player.switchVideo({
            url:video,
            pic: image,
            type:'auto'
          })
        }
      }
    })
  })

```
header.pug

```
header.navbar

```
播放器dplayer

style.pug
```
播放器的样式，直接从github上面拷贝过来
```

# 抓取网站数据
爬虫脚本
分析网页文本，提取文本，模拟浏览器
phantomJS, NightMare, pupeteer

Koa2 子父进程通信


利用pupeteer获取电影列表
豆瓣首页

server/crawler/trailer-list.js
```js
const puppeteer = require('puppeteer')
const url = ''
const sleep = time => new Promise(resolve =>{
  setTimeout(resolve,time)
})

;(aysnc() =>{
  console.log('Start')
  const browser = await puppeteer.launch({
    args: ['--no-sandbox'],
    dumpio:false
  })

  const page = await brower.newPage()
  await page.goto(url,{
    waitUntil:'networkidle2'
  })

  await sleep(3000)
  await page.waitForSelector('.more')
  for(let i = 0 ; i < 1; i++){
    await sleep(3000)
    await page.click('.more')
  }
  const result = await page.evaluate(() => {
    var $ = window.$
    var items = $('.list-wp a')
    var links = []

    if(items.length >= 1){
      items.each((index, item) => {
        let it = $(item)
        let doubanId = it.find('div').data('id')
        let title = it.find('.title').text()
        let rate = Number(it.find('.rate').text())
        let poster = it.find('img').attr('src').replace('s_ratio','l_ratio')

        links.push({
          doubanId,
          title,
          rate,
          poster
        })
      })
    }
    return links
  })
  browser.close()
  console.log()
})()

```
安装
```
$npm i pupeteer
```
## Child Process使用子进程来爬虫
进程模型

server/tasks/moive.js
```js
const cp = require('child_process')
const { resolve } = require('path')

;(async () =>　{
  const script = resolve(__dirname, '../crawler/trailer-list')
  const child = cp.fork(script,[])
  
  let invoke = false

  child.on('error',err => {
    if (invoked) return

    involed = true
    console.log(err)
  })

  child.on('exit',code => {
    if(invoked) return

    involed = false
    let err = code === 0 ? null : new Error('exit code '+ code)

    console.log(err)
  } )

  child.on('message', data => {
    let result = data.result
    console.log(result)
  })

})
```
fork派生子进程
on的方式注册监听函数

server/crawler/trailer-list.js
```js
const puppeteer = require('puppeteer')
const url = ''
const sleep = time => new Promise(resolve =>{
  setTimeout(resolve,time)
})

;(aysnc() =>{
  console.log('Start')
  const browser = await puppeteer.launch({
    args: ['--no-sandbox'],
    dumpio:false
  })

  const page = await brower.newPage()
  await page.goto(url,{
    waitUntil:'networkidle2'
  })

  await sleep(3000)
  await page.waitForSelector('.more')
  for(let i = 0 ; i < 1; i++){
    await sleep(3000)
    await page.click('.more')
  }
  const result = await page.evaluate(() => {
    var $ = window.$
    var items = $('.list-wp a')
    var links = []

    if(items.length >= 1){
      items.each((index, item) => {
        let it = $(item)
        let doubanId = it.find('div').data('id')
        let title = it.find('.title').text()
        let rate = Number(it.find('.rate').text())
        let poster = it.find('img').attr('src').replace('s_ratio','l_ratio')

        links.push({
          doubanId,
          title,
          rate,
          poster
        })
      })
    }
    return links
  })
  browser.close()

  process.send({result})
  process.exit(0)

  console.log()
})()

```
进程的九个问题
什么是进程同步

什么是事件驱动
  就是有事件的时候，才有动作

阻塞


通过豆瓣API，获取详细数据

豆瓣API V2-> 电影API 拷贝示例
需要认证

tasks/api.js
```js
//服务请求库
const rp = require('request-promise-native')

async function fetchMovie (item) {
  const url = 'http://:::'
  const res = await rp(url)

  return res
}

;(async () =>{
  let movies = [
    {
      doubanId:
      title:
    },{
      doubanId:
      title:
    }
  ]

  movies.map(async movie => {
    let movieData = await fetchMovie(movie)

    try {
      movieData = JSON.parse(movieData)
      console.log(movieData.summary)
    }catch (err){
      console.log(err)
    }

    console.log(movieData)
  })
})
```
































































































参考链接：
* [Atom をMarkdownエディタとして整備](https://qiita.com/kouichi-c-nakamura/items/5b04fb1a127aac8ba3b0)

* [《Koa2进阶学习笔记》](https://chenshenhai.github.io/koa2-note/)

* [Koa.js 设计模式-学习笔记](https://chenshenhai.github.io/koajs-design-note/)




