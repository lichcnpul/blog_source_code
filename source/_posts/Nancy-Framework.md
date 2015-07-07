title: 3.2 Nancy Framework
date: 2015-06-29 22:49:49
categories: Thesis
tags: thesis
toc: true
---
## 1 SOA and Web Service
### 1.1 What is SOA
SOA（service-oriented architecture）即面向服务的体系结构。简单来说，SOA就是一种进行系统开发的新的体系架构，在基于SOA架构的系统中，具体应用程序的功能是由一些松耦合并且具有统一接口定义方式的组件（也就是service）组合构建起来的。使用SOA架构的优势在于实现了应用系统的跨平台性和可扩展性。

以我们的指纹认证系统举例，现在我们要实现一个Android手机客户端和一个服务器端，Android客户端通过与服务器端通信调用服务器端提供的API，以实现指纹上传，指纹认证等功能。在传统软件架构模式下，客户端和服务器端开发应处于同一个技术架构当中，比如客户端采用Android（Java），服务器端采用Java EE；或者客户端采用Windows Phone，服务器端采用.net Framework.这种软件架构模式是一种紧耦合的体系结构。其优点在于软件模块紧密协作，调用相同的底层模块，然而这种模式的缺点也十分明显：最大的问题是扩展性差的问题。比如.net开发的服务程序要求客户端同样采用.net技术，这种技术架构已不能满足移动互联网发展的需要。

在移动互联网时代，一项服务往往要为多种客户端提供支持，比如社交软件Line的登录服务，既要为PC客户端提供支持，又要为Android应用提供支持，同时也需要提供iOS的服务支持，甚至还要提供浏览器的相关支持；如果采用传统的体系结构，每添加一个平台都要重写相应的服务，而这些服务所提供的功能几乎是一模一样的，这显示不符合DRY（Don‘t Repeat Yourself）的软件工程原则。在这样的背景下，SOA架构便迅速发展起来。

在SOA架构下，服务器端的每个应用功能都被封装成服务，而这些服务都是平台无关的。客户端与服务器端通过消息传递的方式进行通信，客户端需要调用服务器功能时，直接面向服务接口发送消息，这样就实现了从面向具体技术的体系结构向面向服务的体系结构的转变。无论客户端采用Android技术，还是iOS技术，还是浏览器，抑或是PC客户端，它们都同一调用相同的服务，服务器端不需要做任何改变即可支持多种平台的扩展。这种面向服务的编程模式极大的加强了应用架构的跨平台行和可扩展性，逐渐成为移动互联网时代最主流的架构模式。Web Service是实现SOA最为基础的一项技术之一。
![SOA](/images/thesis/chapter3/2.bmp)
### 1.2 Web Service
Web Service是实现SOA最常用的技术之一。它通过标准的Web协议提供服务，目的是保证不同平台的应用服务可以互操作。（[Web Service](https://en.wikipedia.org/wiki/Web_service)）

Web Service技术经过多年发展，目前出现了两大主要的类型：
1. 基于SOAP的Web Service
2. 基于REST的Web Service

基于SOAP的Web Service：SOAP用来描述传递信息的格式， WSDL用来描述如何访问具体的接口，UDDI用来管理，分发，查询Web Service。SOAP采用了已经广泛使用的两个协议:HTTP和XML（标准通用标记语言下的一个子集）。HTTP用于实现SOAP的RPC风格的传输, 而XML是它的编码模式。使用SOAP，使得Web Service具备了良好的可扩展性，完全与厂商无关，与编程语言无关，与平台无关。

基于REST的Web Service：RT Fielding博士的博士论文《Architectural Styles and the Design of Network-based Software Architectures》奠定了REST风格Web Service的基础。REST 是英文 Representational State Transfer 的缩写。它具有如下特征：
1. 首先REST只是一种风格，不是一种标准
2. REST是以资源为中心的
3. REST的目的是决定如何使一个定义良好的Web程序向前推进
4. REST充分利用或者说极端依赖HTTP协议：
* 它通过逻辑URI定位资源
* 通过分辨 HTTP Request Header 信息来分辨客户端是想要取得资源的哪一种表现形式的数据。
* 在 REST 架构中，用不同的 HTTP 请求方法来处理对资源的 CRUD（创建、读取、更新和删除）操作

![REST API](/images/thesis/chapter3/3.bmp)
REST风格的这些特点，使它比SOAP更加轻量，更充分利用HTTP协议，甚至可以说REST真正表达了HTTP协议的设计原本，REST的出现彻底改变了Web Service的现状，适应了移动互联网的发展趋势，现在主流的移动客户端开发基本都转向了REST风格的Web Service.为了实现Android端的指纹识别客户端，本系统也采用了REST风格的Web Service.
## 2 MVC and Nancy Framework
本系统采用Nancy Framework实现了一个轻量级的REST风格的Web Service。Nancy Framework是基于.net和mono平台的超轻量级Web框架，它遵循MVC框架模式，并设计用来提供REST风格的Web服务。其[官方网站](http://nancyfx.org/)介绍了Nancy具有如下特点：
1. Nancy is a lightweight, low-ceremony, framework for building HTTP based services on .Net and Mono. The goal of the framework is to stay out of the way as much as possible and provide a super-duper-happy-path to all interactions.
2. Nancy is designed to handle DELETE, GET, HEAD, OPTIONS, POST, PUT and PATCH requests and provides a simple, elegant, Domain Specific Language (DSL) for returning a response with just a couple of keystrokes.
3. Nancy is built to run anywhere.

## 2.1 MVC框架模式
Nancy Framework的设计思想来源于Ruby的Sinatra Framework，其基本思想在于MVC框架模式。MVC模式即Model－View－Controller模式，其中：
* Model表示模型，是应用程序中处理应用程序数据逻辑的部分。通常用来封装数据对象存储数据。
* View表示视图，是应用程序中处理数据显示的部分。通常视图数据需要从模型获取。
* Controller表示控制器，控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

![MVC](/images/thesis/chapter3/4.bmp)
上图展示了MVC模式基本工作原理：
1. 首先，用户向应用程序发出请求，等待服务器响应
2. controller接收用户请求，控制器根据请求内容决定分发给哪个model或view处理
3. controller向model请求数据
4. model从database获取数据，并将数据返回给controller
5. controller将model获取的数据发送给相应view
6. view根据model数据填充视图，并将结果返回给controller
7. controller将view返回给用户。

通过MVC框架模式，实现了应用程序业务逻辑和表现的分离，降低了模块之间的耦合性，现在越来越多的应用系统均采用MVC模式，许多框架也都遵循MVC模式，比如Ruby on Rails，Java Spring MVC，ASP.net MVC等等。本系统采用的Nancy Framework也是.net上一个超轻量级的MVC框架。
## 2.2 Nancy架构思想
Nancy Framework是.net平台上一个基于MVC模式的超轻量级Web框架，Nancy Project的项目结构如下图所示：
![Nancy](/images/thesis/chapter3/5.png)
Nancy Framework中Model，Module，Views分别代表了M，V，C。
1. 控制器采用REST风格，其基本模式如下：当用户在浏览器输入http://hostaddress/，Nancy Framework的控制器类会首先根据uri地址匹配相应的controller.这种机制被称为Route机制，是Nancy Framework实现REST风格控制器的核心。当用户以GET方式请求根目录资源时，控制器会根据Route机制查找GET["/"]的控制器，匹配成功以后，由该控制器处理用户请求。控制器可以调用相应的View资源和Model资源最终响应用户请求。
``` csharp
Get["/"] = parameters =>
{
    return View["index"];
};
```
2. 视图以HTML为基本风格，在Nancy官方支持的视图引擎为Radar引擎，其语法大致与HTML相似。
``` html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Fingerprint Web Service Page</title>
</head>
<body>
    Content
</body>
</html>
```
3. 模型一般以Database为模版映射为对象，支持大多ORM框架。

## 3 A System Instance
指纹识别系统的系统详细架构图如下所示：
![System Architecture](/images/thesis/chapter3/6.bmp)
