---
title:  如何在10分钟内创建Chrome扩展程序
date: 2023-09-03 09:28:00
categories:
  - 教程花园
tags:
  - Chrome扩展
  - 实用扩展
  - Google Chrome
  - Manifest V3
  - Manifest V2
description: 您是否曾经考虑过构建自己的Chrome扩展程序，但认为该过程可能太复杂了？好吧，你会大吃一惊！在接下来的几分钟里，我们不仅会介绍Chrome扩展程序的基础知识，还会指导您完成五个简单的步骤来制作自己的扩展程序。
---

> 建造自己的Chrome扩展无异于攀登珠峰?放心,我们会用简单的5步骤来颠覆你的想象!在读完本文后,你不仅会对扩展开发有初步的认知,更能亲手打造属于自己的实用扩展。

## 我们要创建什么

最近,我们见证了AI能力的爆炸式增长。而当这些新的网络伙伴为我们提供前所未有的协助时,也提醒我们:不要与他们分享敏感信息。

我不知道你怎么看,但我的手指往往比大脑更快。所以,为了防止可能的失误,我们将为ChatGPT创建一个"防护装置"。

如果你对“防护装置”这个词感到困惑,它最初指的是用于防止意外激活按钮或开关的挡板。在我们的场景下,它是一个数字守护者,确保我们不会过度分享。

用户可以指定他们认为敏感的词汇或短语列表。如果我们尝试向ChatGPT提交包含任何这些词汇的消息,扩展程序将立即采取行动,禁用提交按钮,并防止我们可能的疏忽。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230903202753.png)

要按照本教程进行操作，您需要一个 ChatGPT 帐户。没有？您可以在[此处免费注册](https://auth0.openai.com/u/signup/identifier?state=hKFo2SBDVzg2VFJCTktxQWlKSEhELWhUYVhaZVhLVndjbFY4Z6Fur3VuaXZlcnNhbC1sb2dpbqN0aWTZIDFiVV9ZaVdsN0tUdDhiM2VfU3lNRkhKdDRrcjZrVTY3o2NpZNkgRFJpdnNubTJNdTQyVDNLT3BxZHR3QjNOWXZpSFl6d0Q)

## 什么是Chrome扩展程序

在我们开始之前,让我们澄清什么是Chrome扩展程序。Chrome扩展程序是一小段旨在增强或修改Chrome浏览体验的软件。扩展程序使用标准的Web技术开发——HTML、JavaScript和CSS——它们的功能可以从简单的工具(如取色器)到更复杂的(如密码管理器)。许多这些扩展程序可以从Chrome网上应用店下载。

注意:对于那些渴望更深入理解Chrome扩展程序的人,Google的官方文档是一个非常宝贵的资源。

值得注意的是,Google Chrome扩展程序可以根据其预期功能采用各种形式。一些具有浏览器操作,由地址栏旁的图标表示,可以快速访问其功能。另一些可能默默地在后台运行,跨所有网页或仅在特定页面上,这取决于它们的设计。

在我们的教程中,我们将关注一种使用内容脚本的扩展类型。该脚本将允许我们与特定页面的DOM交互和操作——在我们的例子中是ChatGPT接口。

### 步骤1:创建扩展程序文件

要启动,我们需要为Chrome扩展程序设置基本结构。我们的名为chatgpt-mollyguard的扩展程序将组织在一个专用文件夹中。这个扩展目录将包含所有必要的文件,使我们的防护装置能够顺利工作。

这里是文件的简要说明:

- 文件夹:chatgpt-molly-guard。这是我们的扩展程序的根目录。我们所有的文件都将驻留在这个文件夹中。

- 文件:manifest.json。我们扩展程序的核心。该文件包含有关扩展程序的元数据,例如其名称、版本和所需的权限。最重要的是,它指定要运行的脚本以及在哪些网站上运行。

- 文件:contentScript.js。顾名思义,这个JavaScript文件包含内容脚本。该脚本可以直接访问网页内容,允许我们扫描敏感词并根据需要修改页面。

- 文件:wordsList.js。一个专门用于包含用户指定的敏感词汇或短语的JavaScript文件。我们将其分离出来,以方便用户自定义其列表而无需深入核心功能contentScript.js。

- 文件:styles.css。一个样式表,为我们的扩展程序添加一些装饰。尽管我们的主要目标是功能性,但让我们的警告或提示看起来不错也无妨!

要开始:

- 在计算机上创建一个名为chatgpt-molly-guard的新文件夹

- 在这个文件夹内,创建上面列出的四个文件。

有了这些文件,我们就可以开始填写细节了。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230903202542.png)

### 步骤2:创建清单文件

清单文件是一个JSON文件,为浏览器提供关于您的扩展程序的基本细节。这个文件必须位于扩展程序的根目录中。

这是我们的清单结构。将此代码复制到manifest.json中:

```json
{
  "manifest_version": 3,
  "name": "ChatGPT Molly-guard",
  "version": "1.0",
  "description": "Prevents submission if specific words are typed into chat window",
  "content_scripts": [
    {
      "matches": ["https://chat.openai.com/*"],
      "css": ["styles.css"],
      "js": ["wordsList.js", "contentScript.js"]
    }
  ]
}
```

清单文件有三个强制字段,即:manifest_version、name和version。其余的都是可选的。

#### 关键清单元素

- manifest_version:指定清单文件格式的版本号。我们使用Manifest V3,这是最新可用的版本。请注意,Google正在2023年积极淘汰Manifest V2扩展。

- name:标识扩展程序的简短纯文本字符串(最大45个字符)。

- version:一个到四个用点分隔的整数,用于标识扩展程序的版本。

- description:描述扩展程序的纯文本字符串(无HTML,最大132个字符)。

- content_scripts:此键指定在打开与URL模式匹配的页面时要静态加载的JavaScript或CSS文件(由matches键指定)。在这里,我们说我们的脚本应在任何以https://chat.openai.com/开头的URL上运行。

在上述字段中,Google将在Chrome的扩展程序管理页面(chrome://extensions/)和Chrome网上应用店中显示您的扩展程序时使用name、version和description。

尽管我们的清单针对我们的需要进行了优化,但许多其他字段可以为您的扩展添加深度和功能。诸如action、default_locale、icons等字段提供了自定义选项、UI控制和国际化支持。

有关manifest.json文件中可用内容的综合概述,请参阅Google的官方文档。

### 步骤3:创建内容脚本

Chrome扩展程序中的内容脚本是在网页上下文中运行的JavaScript文件。它们可以查看和操作它们正在运行的页面的DOM,从而修改网页内容和行为。

这是我们的内容脚本。将以下代码复制到contentScript.js文件中:

```js
const debounce = (callback, wait) => {
  let timeoutId = null;
  return (...args) => {
    window.clearTimeout(timeoutId);
    timeoutId = window.setTimeout(() => {
      callback.apply(null, args);
    }, wait);
  };
};

function containsForbiddenWords(value) {
  return forbiddenWords.some(word => value.toLowerCase().includes(word.toLowerCase()));
}

function updateUI(target) {
  const containsForbiddenWord = containsForbiddenWords(target.value);
  const sendButton = target.nextElementSibling;
  const parentDiv = target.parentElement;

  if (containsForbiddenWord) {
    sendButton.disabled = true;
    parentDiv.classList.add('forbidden-div');
  } else {
    sendButton.disabled = false;
    parentDiv.classList.remove('forbidden-div');
  }
}

document.body.addEventListener('keyup', debounce((event) => {
  if (event.target.id === 'prompt-textarea') updateUI(event.target);
}, 300));

document.addEventListener('keydown', (e) => {
  if (e.target.id === 'prompt-textarea' && e.key === 'Enter') {
    if (containsForbiddenWords(e.target.value)) {
      e.stopPropagation();
      e.preventDefault();
    }
  }
}, true);
```

让我们一步一步拆解。

文件顶部我们声明一个debounce函数。我们将使用它来确保我们不会在用户每次按键时检查禁用的单词。那会有很多检查!相反,我们会等用户停止输入后再做任何事情。我从Josh W. Comeau的网站上取了这段代码,所以你可以查看他的文章以了解它的工作原理。

接下来是一个containsForbiddenWords函数。顾名思义,如果传递给它的文本包含任何我们的禁用词汇,该函数会返回true。我们将两个值都小写,以确保比较不区分大小写。

updateUI函数确定聊天框中是否存在任何禁用的单词。如果存在,它将禁用发送按钮并向聊天框的父div添加一个CSS类(forbidden-div)。在下一步中,我们将利用这一点为用户提供视觉提示。

最后,脚本注册了两个事件侦听器:

- 第一个设置为在keyup事件上触发。它会检查修改的元素是否是我们的目标(聊天窗口),然后调用updateUI函数。多亏了我们的debounce函数,这不会连续运行,而是在输入暂停后过一会才运行。

- 第二个事件侦听器侦听我们目标上的keydown事件。具体来说,它在监视Enter键,如果在文本区域中输入禁用词时按下,它将阻止浏览器的默认操作(在本例中是表单提交)。

这有效地阻止了包含禁用词的消息被发送,既通过禁用发送按钮,也通过拦截和停止Enter按键。

你还会注意到我们使用了事件委托,因为ChatGPT界面是一个SPA。在SPA中,用户界面部分根据用户交互动态替换,这可能会无意中分离绑定到这些元素的任何事件侦听器。通过将我们的事件侦听器锚定到更广泛的DOM并仅针对特定元素进行选择,我们可以绕过这个问题。

### 步骤4:添加一些样式

虽然我们扩展程序的核心功能是阻止某些提交,但重要的是用户必须立即认识到为何阻止了他们的操作。让我们添加一些样式来提供视觉提示,增强用户体验。

这是我们使用的规则。将其添加到styles.css文件中:

```css
.forbidden-div {
  border: 2px solid red !important;
  background-color: #ffe6e6 !important;
}
```

这会在检测到禁用词时向输入区域添加显眼的红色边框和微妙的红色背景。它会立即吸引注意力并表明某些不对劲。通过在父div上切换一个类,我们可以轻松打开和关闭此功能。

值得注意的还有!important标志。在处理你不拥有的网页时(像在这里的ChatGPT),现有的样式可能非常具体。为确保我们的样式具有优先级并正确应用,这个标志会覆盖任何因现有样式特性导致的潜在冲突。

### 步骤5:测试扩展程序

还有最后一步:填充我们的扩展程序应监视的禁用词汇列表。我们可以在forbiddenWords.js中添加这些词汇:

```js
const forbiddenWords = [
  "my-company.com",
  "SitePoint",
  "Jim",
];
```

现在我们的自定义Chrome扩展程序已全部设置好了,是时候测试其功能并确保一切按预期工作。

在Chrome中打开并在地址栏中导航到chrome://extensions/。

打开右上角的“开发人员模式”开关。

单击现在可见的“加载未包装项”按钮。

导航到您的扩展程序目录(在我们的例子中为chatgpt-molly-guard)并单击“选择”。 我们的扩展程序现在应出现在已安装扩展程序的列表中。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230903202348.png)

现在,要测试功能,请导航到ChatGPT,刷新页面,并尝试输入受限制的单词,看扩展程序的行为是否如预期的那样。

如果一切顺利,你应该看到类似下图的画面。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230903202147.png)

识别到禁用词后,扩展程序的工作情况

如果您对扩展程序代码做了任何更改(例如更新单词列表),请务必在扩展程序页面上的扩展程序卡上的右下角点击圆形箭头。 这将重新加载扩展程序。 然后,您需要重新加载扩展程序目标的页面。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230903202250.png)

## 接下来的工作

我们当前的基本Chrome扩展程序已完成其目的,但总有改进的空间。 如果你渴望进一步完善扩展程序并扩展其功能,下面是一些建议。

1. 词汇表编辑的用户界面

目前,我们的扩展程序依赖预定义的受限词汇表。实现用户友好的界面将允许用户动态添加、删除或修改词汇表,这可以通过在单击扩展图标时打开的弹出UI来完成,用户可以在其中管理词汇表。您还需要将词汇持久化到存储。

2. 处理鼠标粘贴事件

虽然我们的扩展程序检测按键,但用户可以通过鼠标右键菜单粘贴敏感信息来绕过此限制。为堵塞这一漏洞,我们可以添加paste事件侦听器(或统一监听input事件)。这将确保无论信息是键入还是粘贴,过滤器都保持健壮。

3. 根据上下文覆盖

屏蔽某些术语可能过于泛泛而论。例如,我可能想屏蔽“Jim”的提及(我的名字),但提及“Jim Carey”时没有问题。为解决此问题,考虑引入一个功能,该功能将在发生下一个提交事件之前禁用molly-guard。

您还可以查看该扩展程序的Firefox版本,其中实现了此功能。

## 结论

我们已经发现,构建自己的Google Chrome扩展程序并非难以攀登的巅峰。我们从一个明确的目标开始:为ChatGPT创建一个保护层,确保敏感信息保密。 在本教程中,我们已经看到,几个文件和一些代码就可以产生一个功能性和有用的浏览器扩展程序。

对于渴望深入探究的人,Google的官方Chrome扩展文档是一个很好的起点。 此外,Chrome扩展迁移指南提供了关于向Manifest V3过渡的见解,这对于2023年即将淘汰Manifest V2的情况至关重要。

现在你已经见识过了过程,我鼓励你完善、增强并根据需要调整扩展程序。