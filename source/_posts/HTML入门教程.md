---
title: HTML入门教程
date: 2023-07-17 20:00:00
categories:
  - 教程花园
tags:
  - 入门
  - 中级
  - 高级
  - html
description: 简单向大家介绍HTML的基本用法
cover: https://www.freecodecamp.org/news/content/images/size/w2000/2023/03/HTML-Blog-Cover-1.png
---

HTML是构建网站的基础,如果你想搭建自己的网页,学习HTML是必不可少的。今天简单向大家介绍HTML的基本用法。
希望这篇博客可以帮助大家快速上手HTML。

## HTML简介

- HTML全称是Hyper Text Markup Language,超文本标记语言。它通过标记标签来标识网页中的文本、图片、链接
等内容。

- HTML文档里的文本都处于不同的标签之间,浏览器会根据标签来解析并显示内容。

- HTML文档使用`.html`作为文件扩展名。一个简单的HTML文档结构如下:

```html
<!DOCTYPE html> 
<html>
<head>
  <title>文档标题</title>
</head>
<body>
  文档内容
</body>
</html>
```

- 浏览器读取这些代码后会解析成可视化的网页。

## 主要特点

HTML是构建网页的基础,其主要特点如下:

1. HTML使用标签来描述网页内容,如`<html>`、`<body>`等。网页文档使用.html或.htm作为后缀。
2. HTML标签通常都是成对出现的,如`<b>`加粗`</b>`,包含开始标签和结束标签。
3. HTML页面主要分为头部`<head>`和主体`<body>`头部包含元信息,主体包含显示内容。
4. 常用的标签有标题标签`<h1>`-`<h6>`、段落标签`<p>`、链接标签`<a>`等。
5. 可以使用`<img>`标签插入图片,`<table>`标签插入表格。
6. `<form>`标签用于定义表单,包含各种输入控件。
7. `<div>`和`<span>`用于页面布局和组织内容。
8. HTML元素可以添加样式来定义布局和外观。
9. HTML5添加了很多新标签和功能,如视频、地图等。
10. 浏览器读取HTML代码并显示出图文网页。
11. HTML简单易学,是网页开发的基础和必备技能。


## 基础标签

HTML有很多标签,常见的有:

- `<h1>`~`<h6>`:标题标签。`<h1>`表示一级标题,`<h2>`表示二级标题等等。
- `<p>`:段落标签。
- `<a>`:链接标签。例如:`<a href="https://www.example.com">This is a link</a>`。
- `<img>`:图像标签。例如:`<img src="image.png" width="200">`。
- `<ul>`和`<ol>`:无序列表和有序列表。
- `<table>`:定义表格。
- `<form>`:定义表单。

以上是一些常用的HTML基础标签,掌握这些就可以编写简单的网页了。

## 页面结构

一个完整的HTML页面主要由三部分构成:

- `<head>`:头部信息,包括页面编码、标题等元数据。
- `<body>`:页面主体内容。
- `<footer>`:页尾信息,通常包括版权声明等。

示例页面结构:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>My Page</title>
</head>

<body>

  <header>
    <!-- 头部内容 -->
  </header>
  
  <main>
    <!-- 主体内容 -->
  </main>

  <footer>
    <!-- 页尾内容 -->
  </footer>

</body>

</html>
```

## 案例

这里给出一些HTML常见的使用案例:

1. 基本页面结构

```html
<!DOCTYPE html>
<html>
<head>
  <title>页面标题</title>
</head>
<body>
  页面内容 
</body>
</html>
```

2. 标题与段落

```html
<h1>一级标题</h1>
<p>这是一个段落</p>
```

3. 文本格式化

```html
<b>加粗文本</b>  
<i>斜体文本</i>
<u>带下划线文本</u>
```

4. 图片与链接

```html
<img src="pic.jpg">
<a href="http://www.example.com">文字链接</a>
```

5. 表格

```html
<table>
  <tr>
    <th>表头</th>
  </tr>
  <tr>
    <td>数据单元格</td>
  </tr>
</table>
```

6. 列表

```html 
<ul>
  <li>无序列表项</li>
</ul>

<ol>
  <li>有序列表项</li>
</ol>
```

7. 表单

```html
<form>
  <input type="text" name="username">
  <input type="submit" value="提交">
</form>
```

8. Div和Span

```html
<div>文档分区</div>
<span>文本内span</span>
```

这些都是HTML实际开发中常见的案例,可以用来学习和应用HTML的基本标签。

了解了基本页面结构,就可以组织起完整的HTML页面了。

## 总结

本文通过简单的示例对HTML进行了概述,内容包括:

- HTML的工作原理
- HTML的主要特点
- 一些常用的HTML标签
- 组织HTML页面的基本结构
- 常见使用案例

希望这篇可以帮助大家对HTML有一个直观的了解,并构建自己的第一个网页。HTML学习还有很多内容,
需要大家积极动手实践。