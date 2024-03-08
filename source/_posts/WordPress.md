---
title: 如何使用代码更改WordPress默认登录URL
date: 2023-09-14 12:28:00
categories:
  - 电子商务
tags:
  - WordPress
  - WP Adminify
  - 安全
  - bot
  - 黑客
  - 防火墙
description: 本文介绍了如何通过代码自定义WordPress的登录页面网址,来增强网站安全性。默认的登录网址非常容易被黑客发现并试图入侵。文章详细介绍了备份网站、定位主题函数文件、添加重定向代码以及测试新的登录网址等步骤。
---

## 引言

WordPress默认的登录页面网址类似于www.yourwebsite.com/wp-admin,这对很多用户来说非常方便。但是,这也使您的网站容易成为黑客或恶意bот的目标。

在本文中,我将指导您完成更改默认WordPress登录URL为更独特和安全的过程。通过这样做,您可以为您的网站添加一个额外的保护层,并减少未经授权访问的风险。

我理解不是每个人都是编程专家,所以不要担心——我会将步骤分解为简单易于遵循的说明。

无论您是初学者还是有经验的WordPress用户,本指南都将为您提供更改登录URL所需的所有信息,无需麻烦。

因此,如果您已准备好增强WordPress网站的安全性,并了解如何使用代码更改默认登录URL,那么让我们直接深入探讨吧!

### 第一步:备份您的网站

在对WordPress站点进行任何更改之前,创建备份都是至关重要的。这可以确保如果在过程中出现任何问题,您可以恢复到以前的状态。您可以使用诸如UpdraftPlus之类的插件或手动备份网站文件和数据库。

### 第二步:访问您的网站文件

要更改默认的WordPress登录URL,您需要修改网站的文件。有两种方法可以访问这些文件:通过FTP客户端或使用托管账户控制面板中的文件管理器工具。选择最适合您的方法。

### 第三步:定位主题的functions.php文件

一旦您访问了网站文件后,请导航到当前在WordPress站点上活动的主题文件夹。在该文件夹中查找functions.php文件。

### 第四步:编辑functions.php文件

在主题的functions.php文件或自定义插件文件中,添加以下代码来执行登录URL重定向:

```php
function custom_login_url_redirect() {
  // 检查当前请求是否是登录页面
  if (strpos($_SERVER['REQUEST_URI'], '/wp-login.php') !== false) {
    // 重定向到自定义登录URL
    wp_redirect('https://example.com/custom-login');
    exit;
  }
}
add_action('init', 'custom_login_url_redirect');
```

将示例URL替换为您实际的自定义登录URL。

### 第五步:测试新的登录URL

保存functions.php文件后,您可以通过访问自定义登录页面来测试新的登录URL。只需在浏览器的地址栏中输入新指定的URL并按回车键。如果一切设置正确,您应该会重定向到WordPress登录页面。

## 使用WP Adminify插件更改登录URL

现在我将引导您完成使用WP Adminify插件更改默认WordPress登录URL的过程。

安装WP Adminify插件后,导航到重定向URL模块选项面板。只需输入新的WordPress控制面板登录URL文本并保存即可。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230914204321.png)

接下来我们测试登录URL。您还可以将尝试使用默认WordPress登录URL的用户重定向到特定页面。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20230914204712.png)

## 总结

综上所述,使用代码更改默认的WordPress登录URL可以极大地增强网站的安全性。通过实施这种简单而有效的技术,您可以防止未经授权的访问并挫败潜在的攻击。我已经讨论了两种方法——使用插件和编辑functions.php文件。两种方法都可靠且有效,允许您选择最符合您的偏好和专业知识的方法。

请记住,将登录URL隐藏起来只是保护WordPress站点的一步。同样重要的是要遵循其他安全最佳实践,如使用强密码、定期更新插件和主题,以及实施可靠的防火墙。