---
layout: post
title: nodejs, npm学习
date: 2018-08-02 11:50:24.000000000 +09:00
---

Node.js 就是运行在服务端的 JavaScript
NPM是随同NodeJS一起安装的包管理工具



安装
sudo apt instal nodejs
sudo apt install npm

https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04


查看版本
```
nodejs -v
npm -v
```

运行一个nodejs程序（交互模式）
```
$ nodejs
> console.log("Hello World")
Hello World
```
运行一个nodejs程序（命令行模式）
```
$ nodejs helloworld.js 
Hello Wolrd
```
使用nvm(Node Version Manager) ，nvm是 Nodejs 版本管理器，它让我们方便的对切换Nodejs 版本

Node.js 创建第一个应用

nodejs不仅是一个应用，同时实现了整个HTTP服务器。
nodejs构成
1. 引入required模块
2. 创建服务器
3. 接收请求与响应请求

```
var http = require('http');

http.createServer(function (request, response) {

    // 发送 HTTP 头部 
    // HTTP 状态值: 200 : OK
    // 内容类型: text/plain
    response.writeHead(200, {'Content-Type': 'text/plain'});

    // 发送响应数据 "Hello World"
    response.end('Hello World\n');
}).listen(8888);

// 终端打印如下信息
console.log('Server running at http://127.0.0.1:8888/');
```

```
$ nodejs server.js 
Server running at http://127.0.0.1:8888/
```

使用 npm 命令安装模块
```
npm intall <Module Name>
```

http模块是nodejs自带的模块，所以刚才的程序中可以直接调用
```
 require('http')
```
安装web框架模块
```
var express = require(`express`)
```
查看安装的模块
```
$ npm list
or
$ npm ls
```

查看具体安装模块的信息
```
check package.json
```

卸载模块，更新模块，搜索模块
```
npm uninstall express
npm update express
npm search express
```
Node.js REPL 交互式解释器
REPL Read Eval Print Loop 类似于Linux下的终端
读取
执行
打印
循环
两次Ctrl+C可以退出

REPL 命令

    ctrl + c - 退出当前终端。

    ctrl + c 按下两次 - 退出 Node REPL。

    ctrl + d - 退出 Node REPL.

    向上/向下 键 - 查看输入的历史命令

    tab 键 - 列出当前命令

    .help - 列出使用命令

    .break - 退出多行表达式

    .clear - 退出多行表达式

    .save filename - 保存当前的 Node REPL 会话到指定文件

    .load filename - 载入当前 Node REPL 会话的文件内容。


回调函数

Node.js 异步编程的直接体现就是回调。
异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。
回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。

阻塞是按顺序执行的，而非阻塞是不需要按顺序的

同步是指一个时刻仅有一件事件在执行。
异步指一个时刻可以有多个事件同时执行。
阻塞指事件执行必须连续，一个事件从开始到结束不能有其他的事件插入执行。
非阻塞指事件可以分成小段执行，不要求从开始到结束连续执行。

Node.js 是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。

### 事件驱动模型
有事件来了才去处理，循环执行，直到没有事件发生

### EventEmitter
Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。
Node.js 里面的许多对象都会分发事件：一个 net.Server 对象会在每次有新连接时触发一个事件， 一个 fs.readStream 对象会在文件被打开的时候触发一个事件。 所有这些产生事件的对象都是 events.EventEmitter 的实例。 

EventEmitter 的核心就是事件触发与事件监听器功能的封装。

EventEmitter 提供了多个属性，如 on 和 emit。on 函数用于绑定事件函数，emit 属性用于触发一个事件,按照参数的顺序执行每个监听器。


### Buffer 缓冲区
定义了一个 Buffer 类，该类用来创建一个专门存放二进制数据的缓存区。

每当需要在 Node.js 中处理I/O操作中移动的数据时，就有可能使用 Buffer 库。原始数据存储在 Buffer 类的实例中。一个 Buffer 类似于一个整数数组

### Buffer Stream

Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。

有四种类型
readable
writable
duplex
transform

管道流
管道提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中。

链式流
链式是通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作。


模块系统
目的是让nodejs的文件可以互相调用
一个nodejs文件就是一个模块

Node.js 中自带了一个叫做 http 的模块，我们在我们的代码中请求它并把返回值赋给一个本地变量。

nodejs有四种不同的模块
从文件模块缓存中加载
从原生模块加载
从文件加载

函数
在JavaScript中，一个函数可以作为另一个函数的参数。我们可以先定义一个函数，然后传递，也可以在传递参数的地方直接定义函数。

匿名函数
我们可以把一个函数作为变量传递。但是我们不一定要绕这个"先定义，再传递"的圈子，我们可以直接在另一个函数的括号中定义和传递这个函数

Nodejs路由
我们要为路由提供请求的 URL 和其他需要的 GET 及 POST 参数，随后路由需要根据这些数据来执行相应的代码。

使nodejs使用自己定义的路由模块

全局对象(Global Object)
JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。

_filename 当前正在执行的脚本的文件名
_dirname 当前执行脚本所在的目录
setTimeout(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。
clearTimeout( t ) 全局函数用于停止一个之前通过 setTimeout() 创建的定时器。
setInterval(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。
setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。

console
	console.log
    console.err
    console.info

process
	process.exit

Nodejs常用工具
util 是一个Node.js 核心模块，提供常用函数的集合，用于弥补核心JavaScript 的功能 过于精简的不足。

util.inherits
util.inspect
util.isArray(object)
util.isRegExp(object)
util.isDate(object)
util.isError(object)

文件系统
文件和目录的常用操作

Nodejs的GET/POST请求
获取GET请求内容
获取 POST 请求内容

工具模块

OS模块
Path模块
Net模块
DNS模块
Domain模块

Web模块
目前最主流的三个Web服务器是Apache、Nginx、IIS。





参考链接: https://www.runoob.com/nodejs/nodejs-tutorial.html



