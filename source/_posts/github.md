---
title: 深入了解GitHub Actions：自动化软件开发生命周期的利器
date: 2023-08-29 14:00:00
categories:
  - 教程花园
tags:
  - Github
  - 触发
  - CICD
  - GitHub Actions
description: 这是一篇通俗易懂的 GitHub Actions 入门教程,通过具体示例带领读者学习如何利用它来自动化软件开发流程。
---

## 引言

在开发者的工作中,编写代码是最重要的任务。然而,有时候他们也需要处理非核心或重复性的任务。为了节省开发人员的时间,自动化重复性任务是非常必要的。通过自动化任务,我们可以提高开发人员的生产力。

随着持续集成/持续部署(CI/CD)流程的兴起,自动化任务的过程变得比以往更加简单。通过CI,我们可以将代码集成到共享存储库中,并运行自动化测试以及早地发现错误。与此同时,CD则可以根据代码和环境变量的变化自动化部署过程。其目标是交付快速可靠的代码。

GitHub也推出了一个名为GitHub Actions的CI/CD流程来自动化任务。它旨在帮助开发人员自动化软件开发生命周期。所以,今天我们将深入了解GitHub Actions的不同方面。

让我们开始吧。

## GitHub Actions

GitHub Action最早于2018年宣布,并在2019年作为一个CI/CD流程公开可用,用于直接从GitHub存储库中自动化软件开发生命周期的各个方面。用于自动化的代码定义在一个YAML文件中。YAML是一种人类可读的数据序列化语言,可用于编写配置文件。

触发GitHub Action的方式可以是拉取(pull)、推送(push)或其他外部触发器。您可以使用GitHub Actions来运行构建、测试或部署网站等任务。

让我们创建一个GitHub Action来更好地理解它。

## 创建GitHub Actions

创建GitHub Action非常简单。在GitHub页面或本地存储库上,创建一个名为.github/workflows的目录。在创建的目录中,您可以创建一个任意命名的YAML文件。YAML文件的扩展名为.yml。因此,文件的名称可以是name.yml。

### YAML文件的基本结构

在顶部,我们需要使用YAML文件中的name关键字提供Action的名称。

```
name: GitHub Actions
```

之后,我们可以添加触发器。触发器可以是拉取、推送或定时触发。要定义触发器,我们使用关键字on。

对于GitHub定义的事件,例如推送,您可以使用以下语法。您还可以添加多个触发器。

```
# 单个触发器
on: [push]

# 多个触发器
on: [push, fork]
```

可以在[这里](https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows)查看可以触发工作流的所有事件。

要定时触发,我们可以使用schedule关键字和cron表达式。

```
on:
  schedule:
    - cron: "0 */12 * * *"
```

Cron表达式可以分解为以下部分:

- `0`:第一个字段是分钟。它表示每小时的第0分钟运行。
- `*/12`:它表示小时字段。它将每12小时运行一次。`*/12`表示每12小时运行一次,而只指定`12`会导致在上午12点和下午12点运行任务。您还可以使用24小时制的时间,例如23表示晚上11点。
- `*`:它是运行的日字段。将每天运行。
- `*`:下一个星号是月份。它将每个月运行一次。
- `*`:最后一个星号定义了星期几。它表示每个工作日运行。它以数字形式表示星期几,星期日是一周的第一天,值为0。使用逗号分隔不同的星期几,例如`0,2,3`。

因此,较简单的语法可以写为:

```
cron: "分钟 小时 日 月 星期几"
```

现在,是时候添加实际的功能了,在触发工作流时运行的功能。YAML中的jobs关键字用于定义不同的作业。

让我们先来看看完整的语法,然后再详细了解它:

```
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

build是作业的名称。其中,runs-on定义了作业将运行的机器。您可以在[这里](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners)找到完整的运行器列表。


现在,我们有了至关重要的steps关键字,用于定义运行工作流时应执行的所有步骤。您可以按顺序定义各个步骤,主要使用name和uses这两个关键字。name关键字用于为工作流中的特定步骤提供描述性名称,而uses关键字用于定义应运行以执行任务的操作或Docker容器。


第一步使用了actions/checkout操作,它将获取存储库、检查引用(如分支、标签或提交SHA)并准备后续步骤的工作区。接下来的步骤是使用所需的工具设置。在我们的例子中,我们使用的是Node.js。之后,我们运行了一个命令来安装依赖项。


最后一步是实际运行代码,产生输出。在我们的例子中,我们使用npm test命令来运行测试。您也可以运行存储库中存在的任何Node.js文件。

```
- name: Update README
  run: node update-readme.js
```

现在,完整的YAML文件的代码如下:

```yaml
name: GitHub Actions

on:
  schedule:
    - cron: "0 */12 * * *"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

## 调试和故障排除

在编写GitHub Actions时,您可能会遇到诸如作业执行失败或语法无效等错误。由于YAML没有内置的调试器,因此调试任何错误变得具有挑战性。但是,有一些方法和工具可以帮助您调试GitHub Actions。以下是一些方法:

- **GitHub Actions扩展**:GitHub为VS Code提供了官方的Actions扩展。它可以帮助您管理和运行Actions。它的验证和代码补全功能可以帮助您编写正确的语法。您可以从[这里](https://marketplace.visualstudio.com/items?itemName=cschleiden.vscode-github-actions)获取该扩展。

- **条件调试**:这种方法不仅适用于YAML,也适用于其他编程语言。通过使用条件来有选择性地启用步骤运行,可以帮助您找到错误的位置。您可以使用`if`条件来进行测试。

- **工作流日志**:GitHub在运行GitHub Actions时会生成日志。这些日志详细说明了每个步骤的执行情况。它可以帮助您了解哪些步骤失败了。您可以通过单击存储库中的“Actions”选项卡来查看日志。

- **Act**:这是一个终端,可帮助您在本地运行GitHub Actions。它可以帮助您在GitHub之前先在本地测试Actions,然后再将其推送到GitHub。这样可以节省时间,因为您不必每次都推送/分叉/拉取来触发Actions。您可以在[这里](https://github.com/nektos/act)查看其存储库。

## 使用GitHub Actions的好处

使用GitHub Actions有以下一些好处:

- **定时作业**:GitHub Actions可以执行定时作业。您可以定义代码并使用GitHub Actions在特定时间段运行它。

- **丰富的生态系统**:GitHub为您提供了与Git集成的生态系统,可以帮助您轻松地将Actions整合到工作流中。关于拉取、推送或分叉的触发器可以轻松地在GitHub上使用。此外,GitHub还有一个市场,提供了许多有用的预构建Action。

- **可扩展性**:正如您所知,GitHub可以管理从小型到大型项目的项目。除此之外,GitHub允许创建多个工作流和Actions,以根据触发器触发不同的作业。

- **安全性**:您可以在存储库设置中定义GitHub Secrets,例如API密钥。YAML文件将访问这些秘密。这样使用环境变量就更加安全。可以使用以下代码访问该秘密:

```
- name: Update README
  run: node update-readme.js
  env:
    GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## 结论

正如我们在本文中所看到的,GitHub Actions可以根据您的需求执行各种任务。我们详细了解了Actions的概念,学习了定义Actions的语法和流程。最后,我们还了解了使用GitHub Actions的一些好处。市场使得快速添加预构建的Actions到您的工作流程变得更加容易。

希望本文对您理解GitHub Actions有所帮助。感谢阅读本文