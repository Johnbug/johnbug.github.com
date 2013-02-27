---
layout: post
title: 计算机安全学：BLP模型和BIBA模型
category: 计算机安全学
---
#今日签到
    
复习今天计算机安全学的课，昨天准备今天的ppt花费了很多时间，但也能大致理解BLP模型和BIBA模型，辛苦队友们了。大家一起学习时焕发的激情让我想到如果我们成立的小组如果能每天都组织去学习，共同探讨一些东西，是提高学习效率的好方法，不再是一个人闭门造车。那些闭门造车的只要弄懂了某些知识就好像得到什么宝一样不和别人分享。这是非常不利的。当然很多牛人对于知识的分享都是比较懒惰的，只能说他们懒惰了！
    
今天的主要知识点是：

    BLP模型；
    BIBA模型；

***

#BLP模型
    BLP是描述访问控制的机密性问题的状态机模型，访问许可通过访问控制矩阵和安全级别来定义，
    安全策略防止信息从高安全级别流向低安全级别，这些策略一般的被称为多级安全（MLS）策略
上面这段话是对BLP模型一个很好的描述。

关键词：
+ 状态机模型
+ 机密性
+ 访问控制矩阵
+ 安全级别
+ 安全策略
+ 安全模型
+ 信息流向

##安全策略

    安全策略为一个安全系统或一组安全系统定义安全；安全策略考虑机密性，完整性，可用性；
    面对特定的安全需求得出的安全策略，在安全系统中定义什么才叫安全，这就是所谓的安全策略。


##安全模型

    表示一个特定策略或一组策略的模型。

安全模型通常是形式化的描述安全策略。为此需要对系统进行建模，有三种主要的模型。
1. 状态机模型
2. 信息流模型
3. 不干扰模型

##状态机模型

    状态机模型是状态以及发生在离散时间点上状态的变化
其实就是状态和状态转移。
###一般状态机模型
####定义状态集：

    A set of states, Q
    An input alphabet Σ
    inital state q0 ∈ Q
    accepting states A ⊂ Q
    transition function δ : Q × Σ → Q
        equivalent to the edges 
![state_Machine1](http://m3.img.libdd.com/farm4/2012/1126/23/078444D44E18596F3E8759E339CA9B1007697180F6503_171_214.JPEG "state_machine1")
####状态机模型描述：

    A state can be good or bad
          secure or insecure
    Transitions from good to bad states are dangerous.
    Two criteria
          Start state be secure
          No transition from secure 
     to insecure
![state_Machine2](http://m2.img.libdd.com/farm5/2012/1126/23/8A8A2B6DAE39EE46F9E9A95BECB067B8E31448725EE3E_167_223.JPEG "state_machine2")

####状态机原则：

    Describe all secure states
    Describe transitions from secure states
    Prove that no transition leads from secure to insecure

If this is possible, the system is provably secure.
Bell-LaPadula is one description of secure states.

符合这种原则的就是安全的状态机；
###具体到BLP模型
####定义状态集

    a set of subjects S
    a set of objects O
    set of access operations A = {execute, read, append, write}
    A set of security levels L, with a partial ordering（偏序） ≤

    A state : (b, M, f), includes
    Access operations currently in use b
    List of tuples (s, o, a), s ∈ S, o ∈ O, a ∈ A.
    e.g (Alice, Bob, read);

    Access permission matrix
    M = (Ms,o)s∈S,o∈O, where Ms,o ⊂ A
    
    Clearance and classification f = (fS, fC, fO) (安全级别分配的集合）
    fS : S → L maximal security level of a subject
    fC : S → L current security level of a subject (fC ≤ fS)
    fO : O → L classiﬁcation of an object

####安全策略
BLP的安全策略在于：

    强制安全策略
    包括Simple Security Property (SS-property)和*-property  系统对所有的主体和客体都分配有上一个访问类属性
    它包括主体和客体的密级和范畴，系统通过比较主体和客体的访问类属性来控制主体对客体的访问

    自主安全策略
    使用一个访问矩阵来表示，主体只能按照在访问矩阵中被授予的对客体的访问权限对客体进行相应的访问
    
#####SS-Property
    A state (b, M, f) satisfies the SS-property if
      ∀(s, o, a) ∈ b, such that a ∈ {read, write}
    fO(o) ≤ fS(s)

在理解这个特性之前，我觉得应该直接的说下信息的不可*“下流”*性比较好。在军用的安全系统中，人有这样的等级：将军，指挥官，士兵。秘密分为：绝密，秘密，公开。将军可以知道三个等级的秘密，指挥官可以知道处绝密以外的秘密，士兵只能知道公开的。也就是说士兵是不能读秘密和绝密的，指挥官也不能知道绝密，意思就是说信息是向上流动的。同样的将军不能写公开的秘密，这句话的意思可以理解为：“将军不能跟士兵谈论，因为自己知道的绝密会被传递出去”
理解了上面的例子，那么这个简单安全特性其实就是在讲：信息“无上读”，即：士兵不能读秘密和绝密。fO(o) ≤ fS(s)的意思就是客体的范畴和安全级别在主体之下或相等。注意write指的是读并且写。这里指的是同级同类别之间的，同个安全级别和同个类别之间能相互地读写。

问题是：某个高级别的主体可以读高级别的信息并写入低级别的客体中，那么信息还是下流了。解决这个问题在于：

##### 星-Property
    A state (b,M, f) satisﬁes the 星-property if  ∀(s, o, a) ∈ b, such that a ∈ {append, write}
            fC(s) ≤ fO(o)
   and
   
    if ∃(s, o, a) ∈ b where a ∈ {append, write}, then ∀o’, a’∈ {read, write}, such that (s, o’, a’) ∈ b   fO(o’) ≤ fO(o)

这里就是在说明：“无下写”的控制策略。依照上面的例子就是：将军不能和士兵谈论。

#####ds-Property
自主安全特性：这个特性的必要性很低，因为他就是用访问矩阵的概念来描述上面两个特性。

所以总结BLP模型就是：“下读上写”

#BIBA模型
BIBA模型主要描述的是完整性，BLP模型描述或者说注重的是信息的私密性。信息的完整性就是说：信息的来源是安全的。保证信息的完整性就是BIBA模型的中心。
###安全策略
BIBA模型主要应用于商业，如银行。举个具体的例子，在学校，任课老师，班长，学生读应安全安级别。老师说：“大家期末都不挂课”。学生会相信。但是如果班长说：“大家期末都不挂课”，大家就不一定相信了。老师亲自给的答案，大家会相信，如果经过班长的手，就会产生疑惑。所以我们为了保证信息的完整性，就规定：信息要“下流”，信息只能是“上读下写”。这样才能保证信息的来源可靠；

    ss-Property 相对于BLP 的是：fO(o) >= fS(s)
    星-Property 对于BLP 的是：fC(s) >= fO(o)

在这个模型中，如果信息上流，那么要使获得来自低级别的信息的高级别的主体降低身份到低级别。所以我们可以说：整个模型只会更“下流”，无法“上流”；

所以总结BIBA模型就是：“上读下写”

#Learn Something Interesting -- SleepSort
今天某美女分享了一个话题：SleepSort。

见代码：

{% highlight bash %}
#!/bin/bash
function f() {
    sleep "$1"
    echo "$1"
}
while [ -n "$1" ]
do
    f "$1" &
    shift
done
wait
{% endhighlight %}

这个东西真是用来娱乐身心的好东西。

还有是分形图：！[分形图](http://m1.img.libdd.com/farm4/2012/1126/23/6F85DEFB1EBAD85D496BCCAD3AAC9EF07FD086AE95681_800_533.jpg "分形图")
神代码：
{% highlight python %}
_                                      =   (
                                        255,
                                      lambda
                               V       ,B,c
                             :c   and Y(V*V+B,B,  c
                               -1)if(abs(V)<6)else
               (              2+c-4*abs(V)**-0.4)/i
                 )  ;v,      x=1500,1000;C=range(v*x
                  );import  struct;P=struct.pack;M,\
            j  ='<QIIHHHH',open('M.bmp','wb').write
for X in j('BM'+P(M,v*x*3+26,26,12,v,x,1,24))or C:
            i  ,Y=_;j(P('BBB',*(lambda T:(T*80+T**9
                  *i-950*T  **99,T*70-880*T**18+701*
                 T  **9     ,T*i**(1-T**45*2)))(sum(
               [              Y(0,(A%3/3.+X%v+(X/v+
                               A/3/3.-x/2)/1j)*2.5
                             /x   -2.7,i)**2 for  \
                               A       in C
                                      [:9]])
                                        /9)
                                       )   )
{% endhighlight %}



