---
layout: post
title: learn about the markdown 
categories: jekyll
---
##特殊字符自动转换   
在写 `<` 和 `&` 时要转成：`&lt;` 和 `&amp;`
> 主要注意在插入url时对`&`的处理～

***
##标题
类 Setext 形式是用底线的形式，利用 = （最高阶标题）和 - （第二阶标题）;   
类 Atx 形式则是在行首插入 1 到 6 个 # ，对应到标题 1 到 6 阶    


***

##区段引用

    > hello world;
    > Johnbug is the most handsome man in the world.
    > My girl is absolutely agree with me.
    >   #include &lt;iostream>
    >
    >       #include <iostream>
    >
    >>      #include <iostream>
    >
    
> hello world;
Johnbug is the most handsome man in the world.

> My girl is absolutely agree with me.

>
>   #include &lt;iostream>
>
>       #include <iostream>
>
>>      #include <iostream>
>

***
##列表

+ first blood
- double kill
* triple kill
1. ultra kill
2. Rampage ！！！
*   Killing Spree 大杀特杀   
    Dominating 主宰比赛   
    Maga Kill 杀人如麻   
    Unstoppable 无人阻挡   
    Wicked Sick 变态杀戮   
    Monster Kill 妖怪般的杀戮   
    God Like 神一般的杀戮   
    Holy_Shit 超神   
*   happy dota!

***
##代码
    #include <stdio.h>
    
    int main(void)
    {
        puts("hello,world");
    }
    
段内代码: `` ` ``

***

##分割线
    * * *
    - - -
    ***
    __________

****

##链接
###行内式
Click to visit my weibo [Johnbug](http://weibo.com/johnbug)

    Click to visti my weibo [Johnbug](http://weibo.com/johnbug)
###参考式
    This is the link to the [Top] [top] Link.

go to [My github blog] [1] and [My github][2];    
这个很好用啊有木有；

***

##图片
    ![Alt Text](path of the picture "Option title")

> for example

![mio](http://attachments.cngba.com/attachments/forum/month_1005/10052019346d7762891d03fb17.jpg "mio")

到目前为止， Markdown 还没有办法指定图片的宽高，如果你需要的话，你可以使用普通的 `<img>` 标签。

***

##代码高亮

看到这两个blog才学会的！[用Jekyll和Pygments配置代码高亮][3] 和 [基于jekyll的github建站指南][4]

{% highlight c %}
#include <stdio.h>    
int main(void) 
{
   puts("hello,world");
}
{% endhighlight %}

***

##文章格式：

    ---	
    layout: post
    title: learn about the markdown 
    tags: [入门,笔记,markdown]
    category: [笔记]
    ---


[1]: http://zzyjohnbug.github.com/
[2]: http://github.com/zzyJOHNBUG/
[3]: http://zyzhang.github.com/blog/2012/08/31/highlight-with-Jekyll-and-Pygments/
[4]: http://jiyeqian.github.com/2012/07/host-your-pages-at-github-using-jekyll/




