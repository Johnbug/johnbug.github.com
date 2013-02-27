---
layout: post
title: 用Jekyll和github写blog的一些理解
category: Jekyll
---

在学校折腾过一段时间，对`github`和`Jekyll`的建站方式和原理一知半解的情况下做了一个很烂的个人blog。寒假回家，突然发现自己的网站竟然出现问题：

>The page build failed with the following error:
>page build failed
>For information on troubleshooting Jekyll see https://help.github.com/articles>/using-jekyll-with-pages#troubleshooting
>If you have any questions please contact GitHub Support.
>
>support@github.com
>https://github.com/contact

在微博上也有人提出这个问题：[@程序员的那些事][1] 参照了这位大哥的[blog][2]的说法，应该是`github`做了某些调整，导致这个问题的发生吧！我用了上面的方法试了下，在本地`jekyll --server`或者`jekyll --safe`都成功的情况下，还是不能生成，估计是其他地方的错误。但我当时很多东西都是一知半解，对jekyll的原理不是很好的理解，于是我搞了一下就放弃了，索性把这个 `repositories`直接删掉了！打算自己再做一个！

如果你要以这样的方式做一个blog，google一下一大堆资料，一步一步做下去其实没有多大的问题！我觉得应该多多理解这种方式的原理。

##加深对github+jekyll建站的理解
简而言之！Jekyll就是一个博客系统，类似`wordpress`。github是一个代码托管服务，github配置好了jekyll，将用户提交的代码用Jekyll建立一个站点！这个站点的域名被指定为：`username.github.com`。所以这种方式的思路就是：`本地配置Jekyll并按照其系统规则建立一个文件结构，上传github，github再远程建立一个站点`

虽然这个blog某些地方写的不是很到位，但对于整理思路还是有帮助的：[P_Chou's Tech Space][3]

很清晰的，我们就可以知道我们需要什么工具了！

####Jekyll本地配置
依照不同的系统的配置方法配置本地，因为Jekyll基于`ruby`，所以我们需要安装`ruby`及其相关，比如`Ruby DevKit`，本地安装`Jekyll`,安装python，有关代码高亮。

我试过Ubuntu和windows的！我觉得Ubuntu环境更适合。但是windows熟悉的人用起来也很方便。推荐的几个blog：
阮一峰：[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门][4]
[像黑客一样写博客——Jekyll入门][5]
[使用Github Pages建独立博客][6]
[在Windows系统配置Jekyll][7]

####git和github的配置和使用
Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。github用的就是git，所以我们上传代码和使用github都是要用的git的，git的使用很简单！
Google一下一大堆的资料，其中的SSH的密钥对，就是用自己的邮箱来生成一个公钥，用自己的密码作为私钥进行身份认证。对同一个库提供多人验证。

##站点结构
做完了这些配置之后，就开始建立一个库，然后建立一个文件结构，典型的目录结构就是：

    _includes
    _layouts
        default.html
    _posts
        2013-2-5-blogging-using-Jekyll.md
    _sites
    _config.yml
    index.html

各部分的功能不赘述。主要是_sites这个目录是最终生成，只要这个命令

    jekyll --server 

成功后，就自动产生了。不要自己去建立。

##设计
自己按照自己的口味做自己喜欢的blog!要学的主要是html和css的基础!
github的好处就是可以去参考别人的代码!现在也很多用github建站.所以可参考的代码是一大堆的。对于`liquid`语法，参考别人的代码也可以收获相当多。我的blog的主题是v字仇杀队，做得感觉还好！但没有一般blog清新的感觉，如果用来提供阅读的环境，并不是很好!先保留着，这几天做得也比较累了！

####推荐Dillinger作为在线markdown编辑器
功能齐全，用起来也顺手！[dillinger][8]

##为什么要写blog？
回顾一下，这次建站的好多知识或者当时的idea并没有很好的保留下来，我想了以前也是，很多东西都是没有很好的计划和应该有的记录和总结，所以我才会一直在忘记！我打算用这两个东西来辅助自己去学会计划，记录和总结！

>Evernote
>我的blog

每次做一件事前要有清晰的思路先写进evernote，然后再做的过程中其中的思路也一并写入。每天11点多就开始总结今天所做的东西。至少写一片blog！希望自己能坚持不懈，培养好这种习惯！人生苦短，如果不留下点什么，总感觉白来一趟。
又是一年！找实习找工作，积累社会经验！今年对我来说太过于重要了！我现在的基础非常的不好！目标也不明确！惟有一点一点的努力才能提升竞争力了！

共勉一句！

>"I went to the woods because I wanted to live deliberately.
>I wanted to live deep and suck out all the marrow of life!
>To put to rout all that was not life, and not, when I had come to die, discover >that I had not lived."
>by Henry David Thoreau



[1]:http://weibo.com/2093492691/zd2xqx9cz?sudaref=python-china.org
[2]:http://youngsterxyf.github.com/BlackWhite/2013/01/08/fix-github-pages-builds-failed/
[3]:http://pchou.info/web-build/2013/01/03/build-github-blog-page-01.html
[4]:http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html
[5]:http://www.soimort.org/posts/101/
[6]:http://beiyuu.com/github-pages/
[7]:http://www.chengyunfeng.com/?p=437
[8]: http://dillinger.io/
