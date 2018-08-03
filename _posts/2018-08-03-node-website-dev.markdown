---
layout: post
title: 使用Node开发网站 实践笔记
date: 2018-08-03 15:50:24.000000000 +09:00

---

Bootstrap 包含了一个响应式的、移动设备优先的、不固定的网格系统，可以随着设备或视口大小的增加而适当地扩展到 12 列。它包含了用于简单的布局选项的预定义类，也包含了用于生成更多语义布局的功能强大的混合类。

现在 Bootstrap 在中型设备中，会查找带有 md 的类，并使用它们。在大型设备中，会查找带有 lg 的类，并使用它们。
sm表示小型设备

bootstrap有一个网格布局

Bootstrap 使用 Helvetica Neue、 Helvetica、 Arial 和 sans-serif 作为其默认的字体栈。

如果需要向任何标题添加一个内联子标题，只需要简单地在元素两旁添加 <small>，或者添加 .small class

Bootstrap 提供了一些用于强调文本的类
```
<small>本行内容是在标签内</small><br>
<strong>本行内容是在标签内</strong><br>
<em>本行内容是在标签内，并呈现为斜体</em><br>
<p class="text-left">向左对齐文本</p>
<p class="text-center">居中对齐文本</p>
<p class="text-right">向右对齐文本</p>
<p class="text-muted">本行内容是减弱的</p>
<p class="text-primary">本行内容带有一个 primary class</p>
<p class="text-success">本行内容带有一个 success class</p>
<p class="text-info">本行内容带有一个 info class</p>
<p class="text-warning">本行内容带有一个 warning class</p>
<p class="text-danger">本行内容带有一个 danger class</p>
```
HTML 元素提供了用于缩写的标记，比如 WWW 或 HTTP。

Bootstrap 支持有序列表、无序列表和定义列表。

还有更多的排版类可以使用
http://www.runoob.com/bootstrap/bootstrap-typography.html

Bootstrap代码
可以使用两种方式显示代码
```
<code></code>
<pre></pre>
<pre class="pre-scrollable"></pre>多行代码带有滚动条
```

表格
```
<table>
<thead>
<tbody>
<tr>
<td>
<th>
<caption>
```
表单

按钮

图片

辅助类

字体图标
图标的网址 http://glyphicons.com/

下拉菜单

按钮组

按钮下拉菜单

输入框组

导航元素
创建一个标签式的导航菜单：
    以一个带有 class .nav 的无序列表开始。
    添加 class .nav-tabs。

导航栏
```
创建一个默认的导航栏的步骤如下：
    向 <nav> 标签添加 class .navbar、.navbar-default。
    向上面的元素添加 role="navigation"，有助于增加可访问性。
    向 <div> 元素添加一个标题 class .navbar-header，内部包含了带有 class navbar-brand 的 <a> 元素。这会让文本看起来更大一号。
    为了向导航栏添加链接，只需要简单地添加带有 class .nav、.navbar-nav 的无序列表即可。
```
面包屑导航
```
面包屑导航（Breadcrumbs）是一种基于网站层次信息的显示方式。以博客为例，面包屑导航可以显示发布日期、类别或标签。它们表示当前页面在导航层次结构内的位置。
```

分页

标签

徽章
```
超大屏幕Jumbotron
本章将讲解 Bootstrap 支持的另一个特性，超大屏幕（Jumbotron）。顾名思义该组件可以增加标题的大小，并为登陆页面内容添加更多的外边距（margin）。使用超大屏幕（Jumbotron）的步骤如下：
    创建一个带有 class .jumbotron. 的容器 <div>。
    除了更大的 <h1>，字体粗细 font-weight 被减为 200。
```
页面标题 page header

### 缩略图
```
本章将讲解 Bootstrap 缩略图。大多数站点都需要在网格中布局图像、视频、文本等。Bootstrap 通过缩略图为此提供了一种简便的方式。使用 Bootstrap 创建缩略图的步骤如下：

    在图像周围添加带有 class .thumbnail 的 <a> 标签。
    这会添加四个像素的内边距（padding）和一个灰色的边框。
    当鼠标悬停在图像上时，会动画显示出图像的轮廓。
```
警告 alert

进度条

多媒体对象(Media Object)

列表组
list-group
list-group-item

面板
面板组件用于把 DOM 组件插入到一个盒子中。创建一个基本的面板，只需要向 <div> 元素添加 class .panel 和 class .panel-default 即可

Well
Well 是一种会引起内容凹陷显示或插图效果的容器 <div>。为了创建 Well，只需要简单地把内容放在带有 class .well 的 <div> 中即可。

### 插件
Bootstrap 自带 12 种 jQuery 插件，扩展了功能，可以给站点添加更多的互动。

使用插件有两种方法
单独引用
编译引用

所有的插件依赖于 jQuery。所以必须在插件文件之前引用 jQuery。

过渡效果（Transition）插件
JS文件：transition.js

模态框（Modal）插件
模态框（Modal）是覆盖在父窗体上的子窗体。通常，目的是显示来自一个单独的源的内容，可以在不离开父窗体的情况下有一些互动。子窗体可提供信息、交互等。

下拉菜单（Dropdown）插件
使用下拉菜单（Dropdown）插件，您可以向任何组件（比如导航栏、标签页、胶囊式导航菜单、按钮等）添加下拉菜单。

滚动监听（Scrollspy）插件
滚动监听（Scrollspy）插件，即自动更新导航插件，会根据滚动条的位置自动更新对应的导航目标。其基本的实现是随着您的滚动，基于滚动条的位置向导航栏添加 .active class。

标签页（Tab）插件

提示工具（Tooltip）插件

弹出框（Popover）插件
```
<a href="#" data-toggle="popover" title="Example popover">
    请悬停在我的上面
</a>
```
警告框（Alert）插件
警告框（Alert）消息大多是用来向终端用户显示诸如警告或确认消息的信息。使用警告框（Alert）插件，您可以向所有的警告框消息添加可取消（dismiss）功能。

按钮（Button）插件

折叠（Collapse）插件

轮播（Carousel）插件

附加导航（Affix）插件

Bootstrap UI 编辑器

可视化编程
http://www.runoob.com/try/bootstrap/layoutit/
























参考链接
https://blog.csdn.net/q132458/article/details/80785248
http://www.runoob.com/bootstrap
