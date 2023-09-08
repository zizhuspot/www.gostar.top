---
title: CSS入门教程
date: 2023-07-19 21:00:00
categories:
  - 教程花园
tags:
  - 入门
  - 中级
  - 高级
  - css
description: 控制网页中的元素的格式，使网页更加绚丽多彩，比HTML更方便有效
cover: https://www.w3docs.com/uploads/media/default/0001/05/6d07a36ebe6d55273b39440f2391f1d7e6d4092a.png
---

CSS是用于设置网页样式和布局的语言,利用CSS可以让网页更美观大方。

## 什么是CSS

- CSS全称是Cascading Style Sheets,层叠样式表。
- CSS描述了HTML元素应该如何在屏幕、纸张等媒体上显示。
- CSS保存为`.css`文件,然后应用到HTML文档中,来设置元素样式。
- CSS的优点:
  - 内容和样式分离,更易维护。
  - 样式可以复用到多个页面。
  - 可以对网页进行统一布局。

## CSS特点

CSS(层叠样式表)是一种样式表语言,主要用于设置网页的视觉呈现效果,其主要特点包括:

1. CSS描述了HTML元素在浏览器中如何显示,比如文字大小、颜色、布局等外观样式。
2. CSS样式作用在HTML标签上,和内容分离,便于维护。可以通过类和id选择器应用样式。
3. 主要的CSS样式有颜色、文字、宽高、边框、背景、布局等,用于美化网站。
4. CSS样式表可以内嵌在HTML中,也可以外部链接文件。推荐外部样式表在多个页面重用。
5. CSS支持控制各类媒体的样式,如打印、屏幕显示等。支持响应式设计。
6. CSS选择器可以非常灵活地控制样式的应用范围,实现复杂网页布局。
7. CSS与HTML协同工作,HTML负责结构,CSS负责外观样式。
8. 浏览器会解析CSS并渲染显示,兼容不同浏览器的CSS调整需要一定技巧。
9. CSS能大幅简化HTML代码,提高开发效率,是Web前端开发的重要技术。

CSS是使网页漂亮的秘密武器。每一个前端开发者都需要学习掌握CSS,以提高网站的视觉表现力。

## CSS基础语法

CSS的基础语法包括规则结构、选择器、属性以及注释等。

### CSS规则结构

CSS规则包含选择器、属性声明块:

```css
selector {
  property: value;
}
```

示例:

```css
p {
  color: red;
  font-size: 14px;
} 
```

选择器指明样式适用的元素,声明块指定要应用的样式。

### CSS选择器

选择器用于选取页面中的元素,常见的有:

- 元素选择器:比如 `p { }`
- class选择器:`.className { }`
- id选择器:`#idName { }`

还有组合选择器、伪类选择器等。

### CSS属性

在声明块中通过属性:值形式定义样式:

```css
p {
  color: red; // 设置文字颜色
  font-size: 14px; // 设置文字大小
}
```

常见属性包括颜色、大小、边框、位置等。

### CSS注释

```css
/* This is a CSS comment */
```

注释内容不会被浏览器解析,用于代码说明。

## 如何使用CSS 

主要有三种方式:

- 内联样式:在HTML元素的`style`属性中设置
  ```html
  <p style="color: red;">This is red text</p>
  ```
- 内嵌样式:在HTML文件`<head>`中使用`<style>`标签包含CSS
  ```html
  <style>
    p {
      color: red;
    } 
  </style>
  ```
- 外部样式表:使用外部`.css`文件,在`<head>`中使用`<link>`标签链接
  ```html
  <link rel="stylesheet" href="styles.css">
  ```

推荐使用外部样式表,这样可以复用样式。

## CSS示例

利用CSS可以改变文字颜色:

```css
p {
  color: blue;
} 
```

改变背景:

```css
body {
  background-color: #f2f2f2;
}
```

设置字体:

```css
body {
  font-family: Arial;
}
```

居中对齐:

```css
p {
  text-align: center;  
}
```

设置图片边框:

```css
img {
  border: 1px solid red;
}
```

以上演示了CSS的一些常用功能。掌握这些可以让网页样式直接跃升一个台阶!

## 常见使用案例

CSS在网页设计中应用非常广泛,这里给出一些常见的CSS使用案例:

1. 文字样式

```css
/* 设置文字颜色、大小、对齐等 */
color: blue;
font-size: 20px;
text-align: center;
```

2. 背景样式

```css 
/* 设置背景颜色、图片等 */
background-color: #f2f2f2;
background-image: url(bg.jpg);
```

3. 超链接样式 

```css
/* 设置不同状态下的颜色、下划线等 */  
a {
  color: hotpink;
}

a:hover {
  text-decoration: none;
}
```

4. 列表样式

```css
/* 设置列表项标记、位置等 */
ul {
  list-style-type: circle;
}
``` 

5. 盒模型

```css
/* 控制元素宽高、边框、外边距等 */
width: 200px;
border: 1px solid gray;
margin: 10px 5px;
```

6. 浮动和定位

```css
/* 设置浮动、相对/绝对定位 */ 
float: left;
position: absolute;
top: 100px;
```

7. CSS3特效

```css
/* CSS3圆角、阴影、动画等视觉效果 */
border-radius: 8px;
box-shadow: 1px 1px 3px #333;
animation: rotate 1s linear infinite;
```

CSS功能非常丰富,这些案例可以帮助大家理解CSS在实际中的应用,进一步掌握CSS的相关技巧。

## CSS高级技巧

CSS提供了一些高级技巧,可以创建更复杂的样式效果和逻辑。

#### 媒体查询

媒体查询可以根据设备特点应用不同样式,实现响应式布局:

```css
@media (max-width: 600px) {
  body {
    font-size: 14px;
  }
}
```

常见的媒体特征包括:

- width - 视口宽度
- height - 视口高度
- orientation - 横屏或竖屏
- resolution - 分辨率 

根据不同特征选取要应用的样式。

#### CSS动画 

使用@keyframes定义动画序列,配合动画属性应用:

```css
@keyframes slideIn {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}

img {
  animation: slideIn 1s ease-in-out; 
}
```

可以创建平移动画、渐变、旋转等效果。

#### CSS预处理器

CSS预处理器在CSS基础上扩展了语法和功能,提高了开发效率。

常用的CSS预处理器包括:

- Sass - 提供变量、混入、函数等功能
- Less - 扩展CSS语法,对CSS进行增强
- PostCSS - 通过JS插件转换CSS代码

预处理器提高了样式代码的可维护性。

## 总结

本文对CSS进行了简明介绍,内容包括:

- CSS的作用
- CSS的特点
- CSS基本语法
- 如何在HTML中使用CSS
- 一些CSS使用示例
- CSS常见使用案例
- CSS高级技巧

希望这篇入门教程可以让大家对CSS有直观的了解,并开始运用CSS使自己的网页更好看!
