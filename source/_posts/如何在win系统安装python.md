---
title: 安装指南:在windows系统上安装pyhton
date: 2023-07-31 16:28:00
categories:
  - web
tags:
  - 编程
  - 开发
  - 平台
  - 应用
  - 程序
  - 服务
description: 本方法也适用于其他Windows版本,不过这里将以Windows 11为例进行演示。
cover: 
---

> 为了确保Python程序在Windows系统上正确执行，必须验证Python是否正确安装并添加到环境变量中。本指南将概述确认系统上是否存在 Python 的步骤，并提供在 Windows 上安装 Python 的详细说明。

## 步骤  1：检查 Windows 上的 Python 安装

在 CMD 或 PowerShell 中输入:

    python --version

如果您看到类似下图的Python版本信息,说明您的系统可以正常运行Python应用程序。具体看到的Python版本可能不同。

![](https://s2.loli.net/2023/07/31/8ASyPJqvr1KxpF4.png)

但是,如果您看到如下的错误信息

![](https://s2.loli.net/2023/07/31/vMaYlzecJgbCBt7.png)

可能表示:您的电脑上未安装Python,Python目录未添加到路径中,这时就需要按照下面的步骤安装Python。

 ## 步骤 2：在 Windows 上安装 Python 首先，您需要访问 Python 官方网站的下载页面：！ 
[Python官方网站](https://www.python.org/) 

![](https://s2.loli.net/2023/07/31/9cVQtI3reZMhHBd.png)

点击下载选项并继续下载最新版本的Python，此页面包含最新版本。只需点击 Python 3.11.4 下载。

![](https://s2.loli.net/2023/07/31/KP2BsfJFIMlVYtE.png)

值得注意的是，在您阅读本文时可能已有更新的版本可用，因此请下载显示的最新版本。下载完成后，您将在指定的下载文件夹中找到一个可执行文件。只需双击该文件即可启动安装向导。

![](https://s2.loli.net/2023/07/31/P7nT2KqtyAcSfVv.png)

出现提示时，选择自定义安装选项。接下来，查看下图中显示的选项，然后单击“下一步”。

![](https://s2.loli.net/2023/07/31/y5HVu96SU8ljYBZ.png)

在随后的界面中，您可以选择符合您的特定要求的各种选项。出于我们的目的，我们将仅安装必要的组件，而不会选择调试符号和二进制文件。

![](https://s2.loli.net/2023/07/31/RDXYBIQzU8SCqOe.png)

建议保留默认安装路径以满足将来的潜在需求，我们直接将 Python 添加到环境变量中。

单击“安装”按钮。

![](https://s2.loli.net/2023/07/31/MtcBeFTxgkXQjDJ.png)

等待安装过程完成，该过程通常需要大约 2-3 分钟。

![](https://s2.loli.net/2023/07/31/KJESbHhdy9RuaW8.png)

如果提示是否禁用路径长度限制，建议选择“确定”。这将解决 Python 对路径长度的限制。

![](https://s2.loli.net/2023/07/31/uoAFiKjyBEM9rNl.png)

不会因此更改而损坏或负面更改任何内容。Python 只支持长路径名。建议关闭路径长度限制。

![](https://s2.loli.net/2023/07/31/xIRmsXg14PWwchY.png)

通过以上步骤，你已经成功安装Python了！

## 步骤 3：如何再次检查Python版本以确认已安装Python

我们现在必须再次确认 Python 是否已正确安装并添加到环境变量的路径中，接下来我们可以使用以下命令检查 Python 在我们的机器上的可用性：

在 CMD 或 PowerShell 中输入:

    python --version

![](https://s2.loli.net/2023/07/31/8ASyPJqvr1KxpF4.png)

如果显示已安装的Python版本，则说明安装成功。

## 步骤 4：检查环境变量

如果要手动检查路径变量，则必须打开高级系统设置。您可以搜索高级系统设置或从控制面板打开它。

![](https://s2.loli.net/2023/07/31/CFqkbMfY9dtrpAL.png)

![](https://s2.loli.net/2023/07/31/HmxMlwysBXVST5q.png)

转到系统和安全。

![](https://s2.loli.net/2023/07/31/8dGPHD1soyEKh2b.png)

单击系统

![](https://s2.loli.net/2023/07/31/EYC6Jo1wU4k7bM5.png)

从这里，单击高级系统设置。

![](https://s2.loli.net/2023/07/31/HjdrIlhnJZYxibk.png)

单击环境变量

![](https://s2.loli.net/2023/07/31/ifysomuwQCHgzGa.png)

单击“路径”，然后单击“编辑”。

![](https://s2.loli.net/2023/07/31/6PWmDA2svhHLi9C.png)

您将看到 Python311 的根目录和 Python311 的脚本目录已经在安装过程中添加，因为我们在安装过程中选中了这些框来执行这些操作。

![](https://s2.loli.net/2023/07/31/Oex6UmDJrHiE2SK.png)

## 按照上述步骤操作，您现在已在计算机上安装了 Python。您现在可以选择任何适合Python的IDE，并开始编写和执行Python代码。

