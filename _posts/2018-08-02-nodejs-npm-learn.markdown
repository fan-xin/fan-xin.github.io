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






参考链接: https://www.runoob.com/nodejs/nodejs-tutorial.html



