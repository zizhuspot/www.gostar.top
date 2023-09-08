---
title: JavaScript 入门教程
date: 2023-07-24 13:28:00
categories:
  - 教程花园
tags:
  - 入门
  - 中级
  - 高级
  - JavaScript
description: JSP简化了动态网页的开发,通过其组件化的特性,可以快速高效地开发数据库驱动的Web应用。它是很多Java Web项目的首选。
cover: https://www.geekboots.com/_next/image?url=https%3A%2F%2Fcdn.geekboots.com%2Fgeek%2Fjavascript-hero-1652702096795.webp&w=2048&q=75
---

JavaScript是一门非常基础和重要的编程语言,对于Website的交互功能都需要依赖它。本教程将通过简单的图文向JavaScript初学者介绍基本语法和使用方法,让大家快速上手。

## JavaScript简介

- JavaScript一种轻量级的编程语言,用于向HTML页面添加交互性。
- JavaScript代码直接插入HTML页面,或者通过扩展名为.js的外部JS文件引入。
- JavaScript可以获取页面元素,操作DOM,也可以响应用户操作等,实现交互效果。
- JavaScript既可以在浏览器运行,也可以通过Node.js等环境运行在服务器端。

一个简单的JavaScript示例:

```html
<script>
alert("Hello World!");
</script>
```

## JavaScript特点

JavaScript是一门非常重要的编程语言,它具有以下关键特点:

1. JavaScript是一种解释执行的脚本语言,用于向网页添加交互性和动态效果。
2. JavaScript可以直接嵌入HTML页面或通过外部文件引用,并由浏览器解析执行。
3. JavaScript可以访问和修改网页的DOM结构,响应用户行为,实现交互逻辑。
4. JavaScript有变量、函数、循环、判断等基础语法,还有面向对象编程能力。
5. JavaScript可以操作网页各种元素、HTTP请求、事件处理等,实现复杂效果。
6. 浏览器提供了调试控制台,可以交互执行和测试JavaScript代码。
7. JavaScript是单线程执行,有异步编程能力,可以避免阻塞线程。
8. Node.js等 Runtime 使用 JavaScript 语言编写应用程度,实现服务端功能。
9. JavaScript拥有大量框架和丰富生态,能简化复杂应用的开发。
10. JavaScript是每一个Web开发者必学的基础语言,也是目前最流行的编程语言之一。

掌握JavaScript对于Web开发极为重要,它赋予网页交互性和动态效果,是一个功能强大和不可或缺的编程语言。

## JavaScript基础语法

JavaScript的基础语法包括变量、数据类型、运算符、函数、流程控制等方面。

### 变量

使用var、let和const关键字声明变量:

```js
let name = 'John';
const age = 20;
```

### 数据类型

JavaScript的数据类型包括:

- Number:数字类型
- String:字符串类型 
- Boolean:布尔类型,true或false
- null:空值
- undefined:未定义
- Object:对象类型

可以使用typeof操作符检查变量类型:

```js
let num = 1;
console.log(typeof num); // 'number'
```

### 运算符

赋值运算符、算术运算符、比较运算符、逻辑运算符等,例如:

```js
let a = 1;
let b = 2;

let c = a + b; // 算术运算符
let d = a >= b; // 比较运算符 
```

### 函数

使用function关键字定义函数:

```js
function add(a, b) {
  return a + b;
}
```

### 条件语句

使用if、else、else if控制代码流程:

```js
if(a > b) {
  // dosomething
} else if(a == b) {
  // dosomething
} else {
  // dosomething  
}
```

### 循环语句

for循环、while循环、forEach等:

```js
for(let i = 0; i < 5; i++) {
  // dosomething
}
```

## DOM和BOM

DOM (Document Object Model) 把文档表示为节点树。

使用方法如getElementsByTagName获取节点:

```js
let elems = document.getElementsByTagName('p'); 
```

修改节点属性,如innerHTML:

```js
elems[0].innerHTML = 'New paragraph';
```

添加事件监听:

```js
btn.addEventListener('click', function(){
  // do something  
});
```

BOM (Browser Object Model) 提供独立于内容的对象,如:

```js
let url = window.location.href; // 获取页面URL
```

## JavaScript数组

创建数组:

```js
let fruits = ['Apple', 'Banana'];
```

数组常用方法:

```js
fruits.push('Orange'); // 末尾添加元素
fruits.pop(); // 删除末尾元素
```

数组遍历:

```js
fruits.forEach(fruit => {
  console.log(fruit);   
});
```

## JavaScript对象

对象表示一组无序的相关属性和方法。

创建对象:

```js 
let person = {
  name: 'John',
  age: 20 
};
```

构造函数:

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
```

## 浏览器本地存储

sessionStorage 和 localStorage API可以在浏览器保存键值对。

```js
// 保存数据
localStorage.setItem('key', 'value');

// 获取数据
let data = localStorage.getItem('key');
```

## AJAX

原生AJAX请求:

```js
let xhr = new XMLHttpRequest();
xhr.open('GET', '/data.json');
xhr.onload = function() {
  // todo
} 
xhr.send();
```

## 错误处理

try/catch 捕获异常:

```js
try {
  // 可能出错代码 
} catch(error) {
  console.log(error);
}
```

## 在HTML中使用JavaScript

创建一个HTML文件,通过`<script>`标签引入JavaScript:

```html
<!DOCTYPE html>
<html>
<body>

<script>
function sayHi() {
  alert("Hi");
}
</script>

</body>
</html> 
```

使用`<script>`标签也可以引入外部的js文件:

```html
<script src="main.js"></script>
```

页面中可以通过`onclick`等给元素绑定JavaScript事件:

```html
<button onclick="sayHi()">Click me</button> 
```

## 浏览器调试

大多数浏览器都提供了调试控制台,可以实时测试JavaScript代码:

通过Console我们可以交互式地运行JavaScript语句。

## 一些简单示例

- 输出内容到页面:
    ```js
    document.write("Hello World!");
    ```
- 弹出警告框:
    ```js
    alert("Warning!");
    ```
- 控制台输出:
    ```js
    console.log("Hello Console!");
    ```
- 等待用户点击确认:
    ```js
    confirm("Continue?");
    ```
- 提取用户输入:
    ```js
    prompt("Your name:");
    ```

通过一些简单的示例可以让JavaScript初学者快速上手,立即在页面看到结果。接下来就可以针对交互功能不断深入学习了。

## 常见使用示例

这里给出一些JavaScript的常见使用示例:

1. 操作DOM

```js
// 获取元素
let div = document.querySelector('div');

// 改变样式
div.style.color = 'red';

// 添加事件处理
div.addEventListener('click', function(){
  alert('Div clicked');
});
```

2. AJAX请求

```js
// 使用Fetch API发送异步请求
fetch('/api/users')
  .then(res => res.json())
  .then(data => {
    // 处理返回数据
  }); 
```

3. 表单验证

```js
// 用户名验证
function validateUsername(){
  let username = document.getElementById('username').value;
  if(username.length < 6){
    alert('用户名不可少于6位');
    return false;
  }
}
```

4. 动画效果

```js
// 使用setInterval实现动画
let id = setInterval(frame, 100); 

function frame() {
  // 每100毫秒执行一次
}
```

5. 网页特效

```js
// 滚动触发固定导航栏
window.addEventListener('scroll', function() {
  let navbar = document.getElementById('navbar');
  if(window.scrollY > 100){
    navbar.classList.add('fixed');
  } else {
    navbar.classList.remove('fixed');  
  }
})
```

这些例子展示了JavaScript在Web开发中的重要作用,可以实现各种交互功能。

## 总结

本教程简单介绍了JavaScript的用途、基本语法、使用方法和一些简单示例,希望可以帮助初学者快速入门。JavaScript是一门强大的语言,需要通过大量的编程实践来掌握和提高。

