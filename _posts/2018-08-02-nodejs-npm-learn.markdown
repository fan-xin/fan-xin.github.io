---
layout: post
title: nodejs, npm学习
date: 2018-08-02 11:50:24.000000000 +09:00
---

#nodejs, npm学习

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

















参考链接: https://www.runoob.com/nodejs/nodejs-tutorial.html



