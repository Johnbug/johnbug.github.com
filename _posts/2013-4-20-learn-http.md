---
layout: post
title: http复习
---

##对不起，老师！
这次去TX一面的惨痛经历让我决心好好地对基础知识认认真真的研究一番。零零散散花了几天的时间理解HTTP协议，过程中很多知识的生疏令我直呼：“对不起，老师。”现阶段自己对HTTP的理解也是停留在“无文档阅读，无实践操作”的阶段！不断Google，不断翻书拿出很零散的知识。但是我对知识全盘理解比较热衷，而且这片blog比较少新的理解和思考，只是对知识的默写罢了，接下来项目的进行可能对自己的理解会有长足的加深，到时一点点补充和改进。必须吐槽自己的学习能力和效率，太低了，但是我是踏实的，认真的！

##Mindmap First
这是本文章的思维导图：
<img src = "/assets/image/HTTP.jpg" width = "600px" height = "550px">

##从万维网讲起，为什么有HTTP？

万维网www`World Wide Web`，可以说是一个一个链接组成的大世界，深入看进去却是一台一台主机通过网络互联的大世界。正是它的出现，因特网才从少数专家玩得起的东西变成了平常人也频繁使用的信息资源。www是一个分布式的超媒体系统，是超文本系统的扩充。

###1.1分布式和非分布式系统

分布式系统体现了系统的内聚性和透明性，各主机对自己的资源有高度的自治性，不考虑链接的一致性和有效性。意思就是说：主机A上的文档X包含了主机B上的文档Y里面的一个链接，那么主机B对该链接做出任何改动，主机A上的链接会失效或不一致。而非分布式系统则相反，其能保证所有链接都是有效和一致的。
	
考虑主机之间的文档传递，可以有这样一种方式：请求与应答。客户端程序向服务器发送请求，服务器响应并传回文档。那么我们需要考虑下面几个问题：
	
>1】怎样标志资源？
>2】主机之间应该遵循怎样的协议进行通信？
>3】如何统一文档？

上述问题的答案闲杂都已经揭晓了，就是URL，HTTP，HTML。这样就是为什么要有HTTP了。

##基于TCP的应用层协议
HTTP的实现基于TCP连接，发现自己TCP的好多内容已经生疏，于是从新回顾了下：

###2.1再次理解TCP
TCP是TCP/IP协议的第四层传输层的内容。因特网中每个主机可以通过IP来确定，但是通信的真正端点却是主机中的进程。而标志端点却不能用进程号来标志，原因是：

>不同的计算机操作系统采用不同格式的进程标识符。
>进程的创建和撤销都是动态的，通信的一方几乎无法识别对方的机器上的进程。

为了统一的标志通信的端点，我们使用端口。端口是应用层的各种协议进程与运输实体进行层间交互的一种地址。不同系统具体实现端口的方法是可以不同的。而我们知道，HTTP的端口是80.
(参考：[端口][1])TCP连接通过可靠的传输协议找到目的端口，将报文面向字节流的方式传递。（TCP的可靠传输真是牛X，再理解一次也要花很的功夫）HTTP的报文封装到了TCP的报文中进行传输。

###2.2HTTP怎么通过TCP连接传输？
一次HTTP通信步骤：

	1.建立TCP连接。
	2.客户端程序（浏览器）发送HTTP请求命令。
	3.Web浏览器发送请求头信息 
	4.Web服务器应答 
	5.Web服务器发送应答头信息
	6.Web服务器向浏览器发送数据 
	7.Web服务器关闭TCP连接 

（参考：[一次完整的HTTP通信步骤（7步）][2]）以此建立较直观的理解。

###2.3Socket连接
Socket是应用层与TCP/IP协议族通信的中间软件抽象层，它是一组接口。在设计模式中，Socket其实就是一个门面模式，它把复杂的TCP/IP协议族隐藏在Socket接口后面，对用户来说，一组简单的接口就是全部，让Socket去组织数据，以符合指定的协议。
（参考：[写给那些让我糊里糊涂的HTTP、TCP、UDP、Socket][3]）

##什么是HTTP协议
协议是指计算机通信网络中两台计算机之间进行通信所必须共同遵守的规定或规则，超文本传输协议(HTTP)是一种通信协议，它允许将超文本标记语言(HTML)文档从Web服务器传送到客户端的浏览器

###3.1报文结构

####请求报文

	方法(space)URL(space)版本(CRLF)
	首部行{
		首部字段名:(space)值(CRLF)
		...
	}
	(CRLF)
	实体主体

3、1、1方法：

	对请求对象的进行的操作叫做方法。
	方法：      意义：
	OPTION      请求一些选项的信息
	GET         请求读取由URL所标识的信息
	HEAD 		请求读取由URL所标识的信息的头部
	POST 		给服务器添加信息
	PUT			在指明的URL下存储一个文档
	DELETE 		删除指明的URL所标识的资源
	TRACE		用来进行环回测试的请求报文
	CONNECT  	用于代理服务器
3、1、2URL:
URL(Uniform Resource Locator) 地址用于描述一个网络上的资源,  基本格式如下

	schema://host[:port#]/path/.../[?query-string][#anchor]
	
	scheme              指定低层使用的协议(例如：http, https, ftp)
	host                HTTP服务器的IP地址或者域名	
	port#               HTTP服务器的默认端口是80，这种情况下端口号可以省略。如果使用了别的端口，必须指明，例如 http://www.cnblogs.com:8080/
	path                访问资源的路径
	query-string       	发送给http服务器的数据
	anchor-             锚

URL 的一个例子

	http://www.mywebsite.com/sj/test/test.aspx?name=sviergn&x=true#stuff

	Schema:                 http
	host:                   www.mywebsite.com
	path:                   /sj/test/test.aspx
	Query String:           name=sviergn&x=true
	Anchor:                 stuff

3、1、3首部字段：

####响应报文

	版本(space)状态码(space)短语(CRLF)
	首部行{
		首部字段名:(space)值(CRLF)
		...
	}
	(CRLF)
	实体主体

3、2、1状态码
（参考[百科-状态码][4]）

首部字段的参考
[1.HTTP协议详解][5]
[2.BeyondTheVoid][6]

###3.2HTTP特点

1.支持客户/服务器模式。
2.简单快速：客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有GET、HEAD, POST。每种方法规定了客户与服务器联系的类型不同。 由于HTTP协议简单，使得HTTP服务器的程序规模小，因而通信速度很快。
3.灵活：HTTP允许传输任意类型的数据对象。正在传输的类型由Content-Type加以标记。
4.无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
5.无状态：HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。 

###3.3版本
超文本传输协议已经演化出了很多版本，它们中的大部分都是向下兼容的。在RFC2145中描述了HTTP版本号的用法。客户端在请求的开始告诉服务器它采用的协议版本号，而后者则在响应中采用相同或者更早的协议版本。
0.9
已过时。只接受GET一种请求方法，没有在通讯中指定版本号，且不支持请求头。由于该版本不支持POST方法，因此客户端无法向服务器传递太多信息。

HTTP/1.0
这是第一个在通讯中指定版本号的HTTP协议版本，至今仍被广泛采用，特别是在代理服务器中。

HTTP/1.1
当前版本。持久连接被默认采用，并能很好地配合代理服务器工作。还支持以管道方式在同时发送多个请求，以便降低线路负载，提高传输速度。

HTTP/1.1相较于HTTP/1.0协议的区别主要体现在：
缓存处理
带宽优化及网络连接的使用
错误通知的管理
消息在网络中的发送
互联网地址的维护
安全性及完整性

（参考[wiki][7]）

RFC 1945定义了HTTP/1.0版本，RFC 2616定义了HTTP/1.1版本。
笔者在blog上提供了这两个RFC中文版的下载地址。
RFC1945下载地址：
http://www.blogjava.net/Files/amigoxie/RFC1945（HTTP）中文版.rar
RFC2616下载地址：
http://www.blogjava.net/Files/amigoxie/RFC2616（HTTP）中文版.rar

HTTP/1.0 每次请求都需要建立新的TCP连接，连接不能复用。HTTP/1.1 新的请求可以在上次请求建立的TCP连接之上发送，连接可以复用。优点是减少重复进行TCP三次握手的开销，提高效率。
注意：在同一个TCP连接中，新的请求需要等上次请求收到响应后，才能发送。
HTTP1.1在Request消息头里头多了一个Host域, HTTP1.0则没有这个域。

(参考[Http协议详解版本二][8])

##细节
[Keepalive][6]
【GET和POST的区别】(参考[HTTP POST GET 本质区别详解][13] , [从HTTP GET和POST的区别说起][14])

##扩展的阅读资料：

[代理][9]
[Cookie][10]
[python的httplib的简单使用][11]
[fiddle的使用][12]

果然到后面就没什么耐心继续写了！晕！！！！！！！

[1]:http://baike.baidu.com.cn/view/1075.htm
[2]:http://stefan321.iteye.com/blog/1397514
[3]:http://blog.csdn.net/xijiaohuangcao/article/details/6105623
[4]:http://baike.baidu.com/view/1790469.htm
[5]:http://www.cnblogs.com/TankXiao/archive/2012/02/13/2342672.html
[6]:http://www.byvoid.com/blog/http-keep-alive-header
[7]:https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE
[8]:http://www.cnblogs.com/xiaopin/archive/2011/07/19/2110210.html
[9]:http://www.cnblogs.com/TankXiao/archive/2012/12/12/2794160.html
[10]:http://www.cnblogs.com/fish-li/archive/2011/07/03/2096903.html
[11]:http://www.cnblogs.com/chenzehe/archive/2010/08/30/1812995.html
[12]:http://www.cnblogs.com/TankXiao/archive/2012/02/06/2337728.html
[13]:http://blog.csdn.net/gideal_wang/article/details/4316691
[14]:http://www.yining.org/2010/05/04/http-get-vs-post-and-thoughts/
