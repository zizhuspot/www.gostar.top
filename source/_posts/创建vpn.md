---
title: 如何构建自己的免费VPN
date: 2023-08-25 08:28:00
categories:
  - 教程花园
tags:
  - Linux
  - 免费VPN
  - OpenVpn
  - Easy-RSA
  - 安全加密
description:  在如今信息如潮的时代，许多人都意识到使用VPN（虚拟专用网络）的重要性。VPN可以提供安全的网络连接，保护个人信息免受黑客和监视机构的侵扰。虽然市面上有许多VPN提供商，但套餐都比较贵，这里你可以自己构建一个免费的VPN。本文将向你介绍如何使用开源软件OpenVPN和Easy-RSA搭建自己的免费VPN。
---

## VPN的作用

VPN(虚拟专用网络)可以提供安全加密的网络通道,保护我们的网络访问隐私和数据安全。商业VPN服务往往需要支付高昂的订阅费用。利用OpenVPN我们可以构建低成本免费的自建VPN。

## 搭建OpenVPN服务器的主要步骤

下面我们看看使用OpenVPN自建VPN的具体步骤:

- 准备Linux云服务器
- 安装配置OpenVPN服务和Easy-RSA
- 生成证书、密钥、TLS验证文件
- 配置服务端的openvpn配置文件
- 设置Linux防火墙规则
- 在客户端导入配置连接

## OpenVPN简介

OpenVPN是一个开源的VPN实现,支持多种加密模式,可以避免数据被监控。它由社区维护,代码开放透明。

下面是详细的搭建教程。

## 步骤1:准备Linux服务器

你可以使用自己拥有的Linux服务器,或者使用像AWS、Google Cloud或DigitalOcean等云服务提供商的免费服务。

具体来说,可以注册AWS免费版EC2实例,选择Amazon Linux 2系统。在实例创建完成后,需要配置安全组规则允许VPN端口的访问。

然后使用提供的公网IP登录服务器:

```
ssh ec2-user@server_public_ip
```
将"username"替换为你登录服务器时使用的用户名,将"server_ip"替换为服务器的IP地址。如果你使用的是云服务商提供的服务器,可以在服务器仪表板中找到IP地址。

## 步骤2:安装OpenVPN和Easy-RSA

OpenVPN支持多种加密模式,可以避免流量被监控。输入以下命令安装:

```
sudo yum update -y
sudo yum install openvpn -y
```

Easy-RSA用来生成证书和密钥。输入以下命令安装:

```
sudo yum install -y easy-rsa
sudo cp -r /usr/share/easy-rsa/3.0.8 /etc/openvpn/
```

## 步骤3:生成密钥和证书

通过Easy-RSA可以生成所需的服务器端证书、密钥、TLS验证文件。

首先初始化PKI:

```
cd /etc/openvpn/easy-rsa/
sudo ./easyrsa init-pki
```

然后依次生成CA证书、服务器证书请求、签名服务器证书:

```
sudo ./easyrsa build-ca
sudo ./easyrsa gen-req server nopass
sudo ./easyrsa sign-req server server
```

设置密码和用户名,后续客户端连接时需要。

## 步骤4:配置服务器

在/etc/openvpn目录下创建服务器端配置文件server.conf:

```
port 1194
proto tcp
dev tun
ca /etc/openvpn/easy-rsa/pki/ca.crt
cert /etc/openvpn/easy-rsa/pki/issued/server.crt
key /etc/openvpn/easy-rsa/pki/private/server.key
dh /etc/openvpn/easy-rsa/pki/dh.pem
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
keepalive 10 120
cipher AES-256-CBC
user nobody
group nobody
persist-key
persist-tun
status openvpn-status.log
verb 3
explicit-exit-notify 1
```

你可以使用Nano编辑器在Linux终端中创建文件:

```
cd /etc/openvpn/
sudo nano server.conf
```

在编辑器中输入上述配置文件的内容......

## 步骤5:启用IP转发

取消/etc/sysctl.conf文件中以下行的注释,以启用IP转发:

```
net.ipv4.ip_forward=1
```

激活更改:

```
sudo sysctl -p
```

## 步骤6:配置Linux防火墙

允许VPN端口1194的UDP流量:

```
sudo firewall-cmd --permanent --add-port=1194/udp
sudo firewall-cmd --reload
```

## 步骤7:客户端配置

生成客户端证书和密钥:

```
cd /usr/share/easy-rsa
sudo ./easyrsa gen-req client nopass
sudo ./easyrsa sign-req client client
```

在此过程中,你需要再次输入用户名,并将"user"作为占位符。然后,在提示时,输入"yes"并输入之前在第三步为服务器的证书和密钥设置的密码。

最后,在`/etc/openvpn/`目录中创建一个名为`client.ovpn`的客户端配置文件,并输入以下内容:

```
client
dev tun
proto udp
remote your_server_ip 1194
resolv-retry infinite
nobind
persist-key
persist-tun
key-direction 1
remote-cert-tls server
tls-auth ta.key 1
data-ciphers AES-256-GCM:AES-128-GCM
verb 3
```

将"your_server_ip"替换为你的服务器IP地址。将客户端证书和密钥复制到本地机器。

## 步骤8:启动服务

服务器上输入以下命令启动OpenVPN服务:

```
sudo systemctl start openvpn@server
```

客户端导入配置文件,通过命令连接VPN:

```
openvpn --config client.ovpn
```
非常棒！你现在已经成功地搭建了自己的免费VPN。

## 结语

本教程通俗易懂地介绍了如何使用开源软件OpenVPN自建免费VPN。逐步涵盖了准备服务器、安装软件、配置证书、编辑配置文件、设置防火墙等搭建步骤。可以作为入门OpenVPN和自建VPN的很好指南,让我们以低成本加强网络安全和隐私保护。通过自己构建免费的VPN，你可以保护个人隐私，浏览互联网时更加安全。请记住，尽管免费VPN可以提供基本的安全性，但它们可能不如付费VPN提供商提供的高级功能和支持。
