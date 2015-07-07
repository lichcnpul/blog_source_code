title: 3. System Architecture
date: 2015-06-26 18:33:45
categories: Thesis
tags: thesis
toc: true
---

# Chapter 3 System Architecture
本章介绍系统总体业务逻辑与架构选择。本章分为2部分，第一部分介绍系统总体业务流程，第二部分阐述跨平台服务器端框架及其工作原理。

## 3.1 Basic Business Process
### 3.1.1 Business Component
业务组件包含4部分：
1. **客户端**: 包含Android智能手机，指纹图片采集模块，特征提取模块，加密模块；

2. **服务器端**: 包含Web Sever，解密模块，认证模块，指纹匹配模块；

3. **第三方组件**: 包含Fingerprint Matcher SDK；

4. **数据库**: 包含指纹图像数据库，用户数据库等。

### 3.1.2 Business Flow
系统总体业务流程如下图所示：
![业务流程图](/images/thesis/chapter3/1.bmp)
系统业务流程包含以下几个过程：
1. **指纹图像采集**: 用户使用Android手机登录客户端，客户端调用照相机和图像采集模块采集用户指纹图像。

2. **图像预处理与特征提取**: 客户端调用特征提取模块对采集到的指纹对象进行预处理，图像增强与特征提取。

3. **图像加密**: 客户端首先接收服务器端发送的QRCode验证信息，然后调用加密模块利用二维码对指纹图像进行加密。

4. **图像上传**: 客户端调用Web API，将加密后的指纹图像上传到服务器端，实现指纹信息的安全传输。

5. **图像解密**: 服务器端调用解密模块对加密的指纹图片进行解密，解密后同时取得验证二维码信息和指纹图像原图片。

6. **用户认证**: 服务器根据解密后得到的二维码认证信息对用户进行认证，确保用户的真实性。

7. **指纹匹配**: 服务器端调用Matcher SDK对用户上传的指纹图片与指纹数据库的图片的对比，获取指纹匹配分数。

8. **验证结果显示**: 服务器将指纹匹配分数返回给客户端，客户端根据匹配分数决定用户认证是否通过。

## 3.2 Architecture Design
### 3.2.1 Object
// waiting to write. (First review something about MVC, Web Service and Nancy, then write this part.)
### 3.2.2 Web Service
// same as 3.2.1
### 3.2.3 Nancy Framework
// same as 3.2.1 
