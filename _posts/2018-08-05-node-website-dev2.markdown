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



















































参考链接：
https://qiita.com/kouichi-c-nakamura/items/5b04fb1a127aac8ba3b0
