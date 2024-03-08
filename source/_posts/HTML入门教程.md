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
description: HTML是构建网站的基础,如果你想搭建自己的网页,学习HTML是必不可少的。今天简单向大家介绍HTML的基本用法。希望这篇博客可以帮助大家快速上手HTML。
---

> 欢迎来到HTML入门教程!本文将带您快速了解和学习HTML的基础知识,包括HTML的概念、基础语法、文本格式化、表单等内容。通过学习本教程,您可以掌握构建简单网页的技能。现在就让我们开始吧!

## HTML简介

HTML是**超文本标记语言**(Hyper Text Markup Language)的简称,是构建网页的基础。HTML通过使用*标记*来对网页内容进行*结构化*,从而实现文本、图片、视频等内容的展示。HTML的发展历史可追溯至1990年代早期,经历了HTML、XHTML、HTML5等版本的演进。现在最新的是HTML5版本。HTML文档主要包含以下基本结构:

```html
<!DOCTYPE html>
<html>
<head>
  <!-- 元数据 -->
</head>
<body>
  <!-- 页面内容 -->
</body>
</html>
```

接下来我们看看HTML的一些基本语法。

## HTML基础

HTML通过标签来定义不同的元素语义。常见的标签包括heading、paragraph、list等。例如:

```html
<h1>This is a heading</h1>

<p>This is a paragraph.</p>

<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

标签可以有属性来定义其行为:

```html
<a href="https://www.example.com">This is a link</a>
```

元素通常可以嵌套来组合使用:

```html
<p>This is a <strong>paragraph</strong> with <em>emphasis</em>.</p>
```

常见标签的有:

- `<h1>`~`<h6>`:标题标签。`<h1>`表示一级标题,`<h2>`表示二级标题等等。
- `<p>`:段落标签。
- `<a>`:链接标签。例如:`<a href="https://www.example.com">This is a link</a>`。
- `<img>`:图像标签。例如:`<img src="image.png" width="200">`。
- `<ul>`和`<ol>`:无序列表和有序列表。
- `<table>`:定义表格。
- `<form>`:定义表单。

以上是一些常用的HTML基础标签,掌握这些就可以编写简单的网页了。

## HTML文本格式化

接下来我们看看HTML是如何进行文本格式化的。

### 标题

通过`<h1>` to `<h6>`标签表示1-6级标题:

```html
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
...
```

### 段落

`<p>`标签用于定义段落:

```html
<p>This is a paragraph.</p>
```

### 列表

无序列表使用`<ul>`和`<li>`:

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

有序列表使用`<ol>`和`<li>`:

```html
<ol>
  <li>First item</li>
  <li>Second item</li>
</ol>
```

### 链接和图片

使用`<a>`定义链接,`<img>`定义图片:

```html
<a href="https://www.example.com/">Example</a>

<img src="example.jpg" alt="Example image">
```

### 表格

使用`<table>`、`<tr>`、`<td>`标签定义表格:

```html
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>John</td>
    <td>20</td>
  </tr>
</table>
```

此外,HTML还提供了大量格式化文本的标签,如`<b>`、`<i>`、`<span>`等。

## HTML表单

HTML使用表单与用户进行交互。表单包含有交互控件,如文本框、下拉菜单、单选框、按钮等。

定义一个简单的登录表单:

```html
<form action="/login" method="post">
  <label>用户名:</label>
  <input type="text" name="username"><br>

  <label>密码:</label>
  <input type="password" name="password"><br>

  <button type="submit">登录</button>
</form>
```

这样就构建了一个简单的包含输入框、标签、按钮的HTML表单。

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

## 总结

本文通过简单的示例对HTML进行了概述,内容包括:

- HTML的简介
- HTML的基本标签和语法
- 文本格式化方法和HTML表单
- 一些常用的HTML标签
- 组织HTML页面的基本结构
- 常见使用案例

希望这篇可以帮助大家对HTML有一个直观的了解,并构建自己的第一个网页。HTML学习还有很多内容,
需要大家积极动手实践。