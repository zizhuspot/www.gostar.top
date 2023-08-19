---
title: 了解跨域资源共享CORS的工作原理及其重要性
date: 2023-08-19 10:28:28
categories:
  - 教程花园
tags:
  - CORS
  - 跨域共享
  - 工作原理
  - 数据
  - 完整性
  - 隐私
description: 跨域资源共享(Cross-Origin Resource Sharing, CORS)是现代网络开发中保证不同域之间安全、受控通信的重要机制。本文将深入探讨CORS的复杂性，揭示其内部工作原理，并探索它如何保护不同网络域之间交换的数据的完整性和隐私。
cover: https://miro.medium.com/max/1130/1*-w04uC0DgFnzUgoKHMRvUA.png
---

## 了解跨域请求

在深入研究CORS的具体内容之前，让我们先了解一下跨域请求的基本概念。

想象一个场景：一个托管在http://localhost:4000/上的网页想要从http://localhost:3000/data的API中获取数据。在过去，这样的交互可能引发数据安全和未经授权访问的担忧。CORS通过添加一层控制和验证来解决这些问题。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230819133709.png)

> 图片显示了一个来自不同源的网页的跨域请求



## CORS的作用

CORS充当了门卫的角色： 将CORS视为虚拟的门卫，驻扎在网络域之间。当发起跨域请求时，门卫会评估请求是否被允许。


源和安全性： 源是协议（HTTP或HTTPS）、域和端口的组合。CORS确保只有来自已批准源的网页才能访问其他域上托管的特定资源。


带有Origin头的请求： 当网页向外部资源发起请求时，它会在请求中包含一个"Origin"头，该头用于指示请求网页的源。


服务器响应带有CORS头： 托管请求资源的服务器会评估传入的"Origin"头。如果服务器配置允许请求的源，它会回复带有CORS头的响应，提供访问权限的详细信息。


## CORS的工作原理

1. **带有Origin标头的请求：** 请求网页向不同域发送请求时，会在请求中包含一个"Origin"头。

浏览器在发起CORS跨域请求时,会自动添加Origin标头,表示请求来源网站,例如:

````js
async function sendCORSRequest() {

  try {

    const response = await fetch('http://api.domain-b.com/data', {

      method: 'GET',  

      headers: {

        'Origin': 'http://app.domain-a.com'

      }

    });

    const data = await response.json();

    console.log(data);

  } catch(e) {

    console.error(e);

  }

}
````

这使得服务器端可以根据Origin值判断请求是否来自允许的域,实现CORS的跨域访问控制。

浏览器自动添加Origin标头是启用CORS的重要一步。

2. **服务器端实现CORS验证:** 服务器检查"Origin"头是否在允许的源列表中。如果请求被授权，服务器将回复特定的CORS头，授予访问权限。

服务器可以校验请求的Origin,确保只有指定的网站可以跨域访问资源,示例如下:

````js
app.get('/data', (req, res) => {

  const allowedOrigins = ['https://app.domain-a.com'];
  
  const origin = req.headers.origin;

  if (allowedOrigins.includes(origin)) {

    res.header('Access-Control-Allow-Origin', origin);
    
    res.status(200);

  } else {

    res.status(403);

  }

});
````

上面做了:

- 定义允许跨域请求的域名allowedOrigins

- 从请求中获取origin标头

- 如果origin在allowedOrigins中

  - 响应CORS头:Access-Control-Allow-Origin

  - 响应状态码200

- 否则返回403未授权状态码

这样可确保只有指定的域名可以请求跨域资源,实现了CORS的服务器端安全验证。

3. **浏览器端验证CORS响应：** 浏览器接收到带有CORS头的响应后，会验证请求的源是否与"Access-Control-Allow-Origin"头中指定的允许源匹配。如果匹配，浏览器允许访问。

浏览器会根据CORS响应头来决定是否允许跨域请求,示例:

````js
async function fetchData() {

  try {

    const resp = await fetch('http://api.domain-b.com/data');
    
    const data = await resp.json();

  } catch(e) {

    console.log(e);

  } 

}
````

上面中:

- 发起跨域请求
- 尝试解析响应
- 捕获请求错误

当接收到响应后,浏览器会检查头信息:

- Access-Control-Allow-Origin 
- Access-Control-Allow-Methods

如果响应头没有正确的CORS信息,浏览器将拒绝此次跨域请求。

这实现了浏览器端对CORS响应的验证,确保服务端允许该跨域请求。

4. **阻止未经授权的访问：** 如果请求的源不在允许的列表中，或者缺少CORS头，浏览器将阻止访问响应。这样可以保护数据免受未经授权的访问。

## 预检请求

预检请求是跨域资源共享(CORS)机制的重要组成部分，浏览器在实际请求之前根据特定条件自动向服务器发送预检请求，以确认服务器是否正确配置以处理跨域请求。


以下是CORS中预检请求的工作原理：


1. **复杂请求：** 预检请求主要用于所谓的"复杂"请求。如果请求满足以下任一条件，则被视为复杂请求：



使用除GET、HEAD或POST之外的HTTP方法。

使用
setRequestHeader()
方法设置自定义头。

以简单文本数据以外的形式（例如JSON、XML）发送数据作为请求体。


2. **预检请求：** 当浏览器检测到跨域请求为复杂请求时，在实际请求之前自动向服务器发送预检OPTIONS请求。该预检请求包含以下头部信息：



Origin
：请求网站的源。

Access-Control-Request-Method
：实际请求的HTTP方法。

Access-Control-Request-Headers
：请求中使用的自定义头列表。


3. **服务器响应：** 服务器应配置以用适当的CORS头回复预检请求。这些头部信息告知浏览器是否允许实际请求。相关的头部信息包括：



Access-Control-Allow-Origin
：指定允许访问资源的源。该头部必须与请求网站的源匹配，或者设置为
*
以允许任何源。

Access-Control-Allow-Methods
：指定实际请求允许的HTTP方法。

Access-Control-Allow-Headers
：指定实际请求允许的自定义头。


4. **浏览器决策：** 根据服务器预检请求的响应，浏览器决定是否继续进行实际请求。如果服务器回复了适当的头部信息，指示允许实际请求，浏览器将发送实际请求。如果服务器未提供必要的头部信息或明确拒绝请求，浏览器将生成CORS错误，并不发送实际请求。


5. **实际请求：** 如果预检请求成功，浏览器将以适当的头部信息向服务器发送实际请求。服务器处理该请求并作出响应。


需要注意的是，预检过程通过确保服务器明确允许跨域请求并指定允许的方法和头部信息，增加了一层额外的安全性。这有助于防止未经授权的访问和潜在的安全漏洞。


在设置CORS时，确保服务器正确处理预检OPTIONS请求，并以适当的CORS头回复，指示实际请求允许的源、方法和头部信息。


## 结论

- CORS充当跨域请求的门卫角色,验证每个请求的来源,只允许授权的源访问资源。这大大提高了跨域网络通信的安全性。

- 通过自动处理预检请求、响应头等机制,CORS将复杂的跨域通信复杂性封装起来。这简化了开发者的工作。

- CORS为不同域间的数据交换建立了可控的安全通道,有效防止了数据泄露或被非法访问的风险。

CORS为跨域请求添加了必要的验证,使跨源网络通信更安全、简单且私密。它已成为现代Web应用必备的安全基石,值得每一位开发者投入时间去深入理解。

