---
title:  Python异常处理指南
date: 2023-08-14 09:28:00
categories:
  - 语言驿站
tags:
  - python
  - 异常
  - try
  - except
  - 代码
  - 语法错误
description: 在本文中,我们将学习如何处理Python中的错误和异常,这被称为“异常处理”。
---

## 引言

通常在Python编程中会遇到两类错误:语法错误和异常。

任何由无效语法、缩进或编程结构引起的错误通常被视为语法错误。当发生语法错误时,程序会在语法错误发生的位置崩溃。

异常是扰乱计算机程序正常流程的异常情况。当发生异常时,我们需要处理这些异常,以确保我们的程序不会突然崩溃。

异常处理是在计算机程序中实施检查以处理执行程序时可能发生的错误(无论预期或非预期)的过程。

## Python异常处理

Python与其他编程语言一样,都有处理执行过程中发生的异常的方法。这意味着异常会被优雅地处理:我们的Python程序不会崩溃。当一个语法上正确的程序在运行时发生错误时,Python会使用try和except语句来捕获和处理异常。

由于大多数异常都是可预期的,所以在我们的Python程序中需要对异常处理进行更具目标性或具体化。具体的异常处理使程序调试更容易。

## 一些标准的Python异常

Python有一系列内置异常用于处理不同的异常情况。下面是一些内置的Python异常:

1. Exception - 所有自定义异常也应该派生自这个类
2. ArithmeticError - 由各种算术错误引发的内置异常的基类
3. AssertionError - assert语句失败时引发
4. AttributeError - 属性引用或赋值失败时引发
5. ImportError - 导入语句加载模块时遇到问题时引发
6. IndexError - 当序列下标超出范围时引发
7. KeyError - 当映射(字典)键在现有键集中没有找到时引发
8. NameError - 当本地或全局名称未找到时引发
9. ValueError - 当操作或函数接收到类型正确但值不合适的参数时引发
10. ZeroDivisionError - 当除法或取模的第二个参数为零时引发

## 用try和except语句处理Python异常

try和except块用于Python中的异常处理。语法形式如下:

```
try:
    # 可能引发异常的代码
except:
    # 处理异常的代码
```

try块包含可能引发异常的代码部分,except块包含处理异常的代码。

我们来看一个简单的例子:

```
print(3/0)
```

上面的代码会生成一个错误信息,同时程序终止:

```
ZeroDivisionError: division by zero
```

可以通过下面的方式来处理这行可能抛出异常的代码:

```
try:
    print(3/0)
except ZeroDivisionError:
    print("不能除以零")
```

在上面的例子中,我们把第一个print语句放在try块中。try块中的代码将引发异常,因为除以零是没有意义的。except块将捕获在try块中引发的异常。try和except块经常一起用于Python中的异常处理。与之前生成的错误消息不同,我们只是在控制台中简单地打印了“不能除以零”。

## 多重Python Except块

有时候我们会使用两个或多个except块来捕获并区别处理不同的Python异常。多个except块可以帮助我们捕获特定的异常并在程序中区别对待:

```
try:
    number = 'one'
    print(number + 1)
except TypeError:
    print("不能连接字符串和整数")
except NameError:
    print("名称未定义")
```

上面代码的输出是:

```
不能连接字符串和整数
```

从上面的例子可以看出,我们定义了两个except块来指定要处理的异常类型:TypeError和NameError。try块中的第一个print语句抛出了TypeError异常。Python解释器会检查每个子句以找到适当的异常类,在这里是由第二个except块处理的TypeError。“不能连接字符串和整数”被打印到了控制台。

如果一个异常已经发生,try块中的第二个print语句会被跳过。然而,任何在最后一个子句之后的代码都会被执行:

```
try:
   # 代码
except:
   # 代码

# 后续代码
```

## 通用的Python except块

我们可以有一个通用的except块在Python中捕获所有的异常。通用except块可以与其他特定的块一起在我们的程序中使用来捕获未处理的异常。把最通用的子句放在所有特定的块之后是合乎逻辑的。这会在发生未处理的异常时被触发。

## raise语句

有时在我们的Python程序中,我们可能想在某些条件不匹配我们要求时使用raise关键字引发异常。raise语句由关键字本身、异常实例和可选参数组成。

## else子句

else子句可以添加到标准的try和except块中。它放在except子句之后。else子句包含如果try语句没有引发异常时我们想执行的代码。

## finally子句

finally子句可以添加到try和except块中,并在必要时使用。finally子句中的代码无论是否发生异常都会执行。

## Python中的自定义异常

内置异常很好,但我们的软件项目可能需要自定义的异常。Python允许我们创建自定义异常来满足我们的需求。

自定义异常是通过继承Python的Exception类派生的。自定义异常的语法如下:

```
class CustomException(Exception):
    pass

try:
    pass
except CustomException:
    pass
```

## 总结

在本教程中,我们了解了语法错误和异常之间的主要区别。我们还看到语法错误或异常会扰乱我们程序的正常流程。
我们还了解到try和except语句是Python中处理异常的标准语法。合理利用异常处理可以让我们的Python程序在出现错误时优雅地处理,而不是直接终止。通过识别各种异常情况,我们可以让程序按我们的意图继续运行。
