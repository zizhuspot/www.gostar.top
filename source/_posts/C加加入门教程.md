---
title: C++语言编程入门教程
date: 2023-08-11 14:28:00
categories:
  - 教程花园
tags:
  - C++
  - 基础
  - 编程
  - 功能
  - 初学者
description:  C++是一种通用的编程语言,拥有高性能、高扩展性等优点,在游戏、操作系统、企业应用等开发中广泛使用。本教程将介绍C++的基础语法和功能,帮助初学者学习C++编程。
cover: https://images5.alphacoders.com/430/430890.jpg
---

## C++基础

C++是一种通用的编程语言,由Bjarne Stroustrup于1979年在C语言基础上设计开发。C++发展自C语言,是一门面向对象的程序设计语言,兼具高级语言和低级语言的优点。C++拥有函数、类、封装、继承、多态等面向对象特性,也可以进行系统级编程。

要开始C++编程,你需要一个代码编辑器,比如Visual Studio、Visual Studio Code等,也可以使用记事本编写代码。接下来我们用一个简单的“Hello World”程序展示C++的基本语法结构:

```cpp
#include <iostream> // 包含输入输出流头文件

using namespace std; // 使用std命名空间

int main() { // 主函数
  cout << "Hello World!"; // 输出 
  return 0; // 返回值0表示正常退出
}
```

这个简单的程序演示了`#include`包含头文件、`main()`主函数、`cout`进行输出的用法。编译并运行后,程序将输出"Hello World!"。

## C++特点

- 面向对象:提供类、封装、继承等特性
- 过程化:保留了C语言中的过程化编程功能
- 混合编程:支持面向对象编程和过程化编程
- 性能高效:编译执行效率高,可用于开发性能敏感应用
- 编译型语言:代码需先编译后执行

## C++基础语法

### 变量和数据类型

C++支持基础类型:

```cpp
int a = 10; // 整型
double b = 3.14; // 浮点型
bool c = true; // 布尔型
char d = 'A'; // 字符型
```

### 运算符

C++支持算术、赋值、比较、逻辑等运算符:

```cpp
int sum = a + b; // 算术运算符
a += 2; // 赋值运算符
a == b; // 比较运算符
!(a && b); // 逻辑运算符
```

### 流程控制

if语句、循环:

```cpp
if (a > b) {
  // todo
} else if {
  // todo 
} else {
  // todo
}

for (int i=0; i<10; i++) {
  // todo
}
```

##  C++面向对象编程

### 类和对象

定义类:

```cpp
class Person {
public:
  string name; 
  int age;
  
  void printInfo() {
    // todo
  }
};
``` 

创建对象:

```cpp
Person p1; 
p1.name = "John";
p1.age = 20;
```

访问成员通过`.`运算符。

### 封装、继承、多态

封装通过public/private修饰符控制访问;

继承通过`: public`实现继承;

多态通过虚函数实现。

## C++数组和字符串

定义数组: 

```cpp
int nums[10]; 

string strs[2] = {"hello","world"};
```

字符串常见操作:

```cpp
string s = "hello";

s.size(); // 长度
s.find("lo"); // 查找
s.substr(2,3); // 截取字符串
```

##  C++函数

定义函数:

```cpp
int add(int a, int b) {
  return a + b;
}
```

内联函数:

```cpp 
inline int add(int a, int b) {
  return a + b; 
}
```

##  C++模板

函数模板:

```cpp
template <typename T>
T min(T a, T b) {
  return a < b ? a : b; 
}
```

类模板:

```cpp
template <class T>
class Stack {
  // 栈实现 
};
```

## C++异常

异常处理:

```cpp
try {
  // 可能抛异常的代码
} catch (Exception e) {
  // 处理异常
}
``` 

抛出异常:

```cpp
throw Exception("Error occurred"); 
```

## C++文件操作

输出到文件:

```cpp
ofstream f("test.txt");
f << "Hello World";
f.close();
```

从文件输入:

```cpp
ifstream f("test.txt");
string line;
while(getline(f, line)) {
  cout << line << endl;
}
f.close();
```

## C++ STL

Vector动态数组:

```cpp
vector<int> vec;
vec.push_back(1);
vec.size();
```

List链表:

```cpp
list<string> mylist;
mylist.push_back("a");
mylist.pop_front();
```

Map字典:

```cpp 
map<string, int> dict;
dict["key"] = 1;
dict["key"]; // 访问元素
```



![](https://s2.loli.net/2023/08/11/DnlOgs94Fe5rdUM.png)


## 结语

C++的这些关键特性使C++成为一门功能强大、性能优良的编程语言。这些基础知识可以帮助初学者开始C++编程之旅。希望本教程对你有所帮助!你可以在此基础上不断深入,掌握C++所有强大的功能。