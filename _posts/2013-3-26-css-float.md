---
layout: post
title: css float的详解
---

##摘要
css有三种定位体系，`normal flow`，`float`，`absolute positioning`。普通流是普遍的布局定义，而float和绝对定位都是脱离了普通流。我在这片文章中说明我对float的理解：

+ 什么是float及怎么影响其他元素及其原理
+ clear属性
+ 怎么清除float

##let it float
规范是这样描述float的：

>In the float model, a box is first laid out according to the normal flow, then taken out of the flow and shifted to the left or right as far as possible. Content may flow along the side of a float.

也就是说，一开始float元素先按照normal flow那样布局，然后再从normal flow中抽出来，尽可能往最左或最右布局。然后文档内容围绕着它，而不能覆盖(除非设置了margin)。然后根据这个描述：
 
>Since a float is not in the flow, non-positioned block boxes created before and after the float box flow vertically as if the float did not exist. However, the current and subsequent line boxes created next to the float are shortened as necessary to make room for the margin box of the float.

可以这样解释float的原理：首先，按照normal flow布局，但生成了一个块级框，也就是说生成了一个bfc！所以它与外界失去了联系，不会发生外边距碰撞重叠等等。这种块级框对行框造成了shorten作用，所以normal flow中这几行的行框就被缩短了，于是造成了文档的环绕排布。然后再从normal flow上去掉漂浮框。其上即可放置其他normal flow的东西了。在同一个bfc中是不能覆盖float的！
具体的float的布局原则可以参考[w3c规范][1]或者[w3chelp][2]。

##clear
规范的描述是：

>This property indicates which sides of an element's box(es) may not be adjacent to an earlier floating box. 

原理：
在css2.1之前是通过增加元素的margin-top来清除掉浮动，现在是通过增加`clearance`来清除的。规范中说的很清晰：要比较这两个值来计算clearance的大小！

	c1 = h - m2
	c2 = max(m1,m2)-m1-m2 = max(-m1,-m2)

c = max(c1,c2)

可以看看这个例子：
{% highlight css %}

div#a{
	height: 100px;
	width: 200px;
	background: red;
	margin-bottom: 60px;
}
div#b{
	height: 100px;
	width: 50px;
	margin:0;
	float: left;
	background: blue;
}
div#c{
	clear: left;
	height: 100px;
	width: 200px;
	background: yellow;
	margin-top: 150px;
}

{% endhighlight %}

现在的c1 = h - m2 = 100 - 150 = -50; c2 = max(-m1,-m2) = -60 所以c = -50 可以自己调节h，m1，m2的大小来查看效果。

##清除浮动（闭合浮动）
参考这位[gduter][3]的文章，的确讲得很好。收获很大！
为什么在尾部添加空div即可闭合浮动呢？根据上面讲的，父级的div会被填充clearance，造成了闭合起来的“假象”，其实没有生成bfc是不可能真正地闭合浮动的，但是这种方法比较经典。
由于ie的各种bug，也导致了其他的方法。

##负外边距
规范中讲到float是不能超过父元素的，但用了负外边距，会造成重叠。到底为什么不会造成环绕，我也不是很懂。

##浮动！浮动！
巧用好浮动的确能为我们布局管理省了很多功夫！看到一个很好玩的东西：
[九宫格][4]



[1]:http://www.w3.org/TR/CSS2/visuren.html#floats
[2]:http://w3help.org/zh-cn/kb/011/
[3]:http://kayosite.com/remove-floating-style-in-detail.html
[4]:http://litten.github.com/blog/blog/2012/12/14/css-jiugongge/