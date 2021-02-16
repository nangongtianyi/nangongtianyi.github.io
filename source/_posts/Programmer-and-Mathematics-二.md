---
title: "Programmer-and-Mathematics-二"
date: 2021-01-30 10:26:47
tags:
categories:
    - 文章
mathjax: true
---

# 论步伐与耐心

在上一章中，我们学到了很多东西，最为突出的是我们了解了学习陌生的数学知识时会有多慢。作者提到，每次看到定义或定理时，都必须停住写下来以便好好的理解。这与编程没什么不同，有经验的开发者都知道何时启动REPL或调试器，或者写测试程序来隔离新功能，测试其工作原理。

<!-- more -->

对我们来说，数学与编程最大的区别就是数学没有REPL或者调试器，没有参考实现。数学家经常通过相互交流来绕过这个障碍，作者鼓励我们找一个朋友一起通读这本书（:)似不似为了多卖两本书）。William Thurston在《关于数学的证明和进步》中写道：“数学知识嵌入到了思考某个主题的人们的思想和社会结构中，书籍和论文对此提供了支持，但是您走的越高，知识的主要来源与教科书的距离就越远。”

如果你是自己阅读这本书，那么你必须扮演如下的角色：开发者、测试人员和编译器。当你想出新的点子提出问题时，你是一个开发者，当你阅读定理和定义时，你是一个测试人员，当你检查你的直觉和预感是否有错误时，你是一个编译器。对新手和专家而言，这通常会使你阅读数学的速度变慢。数学家们通常使用铅笔和笔记本来非常方便的阅读。

当你初读定理时，你会感到非常困惑。作者再次提到：铁律就是你会困惑，例外是你什么都懂。数学文化的特点就是你什么都不懂时会感到十分的舒适。但这是一种卑微的生活。一旦你弄明白了一些不清楚的地方，你的理解就会取得进步。最容易的方式就是写下大量的示例，但并不是总能做到这一点。我们已经看到了这样的例子，那就是不可能有一个非零多项式其根的个数大于其次数。

作者在这里举了一个例子，这里不再引述，意在阐述这样一个事实：当你尝试学习的数学越多，你越会觉得自己越一无所知。我们也要尝试做到这一点：我显然没搞明白，但我已经接受了，会慢慢尝试理解。

作者在这里又举了几个例子，当我们想学习数学，而这些知识又十分庞大，可能需要花费我们大量的时间时，请务必记住两个事情：洞察力像一个阶梯，每一个梯级都是有用的，所以不要怕一些小事特别花时间，只要它是有用的就行；当我们练习阅读和吸收的数学知识越多，我们掌握的就越好，因为在这个过程中，会锻炼我们解决问题的能力。

最为重要的一点：兴趣是最好的老师。

# 集合

本章将为本书的其余部分奠定基础，这章的大部分专门讨论集合和集合之间函数的数学语言。集合和函数不仅仅是计算机科学中大多数数学的基础，还是所有数学家之间的通用语言。集合是数学的建模语言，将现实世界的问题转换成数学语言的第一种，也通常是最简单的方式就是以集合和函数的方式写下问题的核心概念。然而集合论中有许多新的术语，理解这些的最好方式就是写下来大量的示例。

将想法转换为集合的语言后，就可以利用许多现有的工具和技术来处理集合。这样一来，所要做的工作就是从数学的角度来了解这些技术。软件也大致是这样，我们需要学习如何将复杂的问题分解成为简单的、可测试的、可维护的功能，无论使用哪一种编程语言都可。软件随业务的变化而灵活对业务规则进行建模的过程也是如此，集合是一项基本的能力。

在本章的最后，我们将看到名为稳定婚姻的app的完整建模过程，该过程是数学和经济学跨学科领域的一部分。在经济学中，有时市场不能将金钱用作交换媒介，在这些情况下，必须寻找其他机制使市场有效运作。我们将看到的示例是医疗居住匹配市场，但类似的想法也适用于器官捐赠和住房分配等市场。正如我们所看到的那样，对这些系统进行建模以使其能够进行数学分析，只需要我们能够流利的使用集合和函数。

## 集合，函数以及它们的关系

集合是唯一对象的集合。我们应该已经在软件中见过类似的概念，例如python中的set，Java中的HashSet以及C++中的unordered_set，功能上它们是等效的，都是没有重复的对象集合。在本章中，不讨论集合的技术细节，即不讨论对象的进入离开，只关心数学集合的相关特性。

开始了解集合的第一件事就是如何描述集合，大多数方法都是隐式的，而其中最简单的就是用语言描述，例如能被7整除的整数集等。分析数学对象的目的经常是找到一种比隐式描述更好的使用集合来进行更有效描述的方法，但从隐式定义开始研究集合是一个不错的起点。

描述集合的一种较为熟悉的方法是使用集合生成器符号。这种风格对开发人员比较友好，因为这种形式存在于多种编程语言中，例如定义所有可能被7整除的非负数的集合：
$$
S = \{ x:x \in \mathbb{N},{\text{x is divisible by 7} }\}
$$
**定义4.1：**集合$A$的基数或大小，用$|A|$表示，是集合$A$中元素有限时元素的个数，否则$A$有无效的基数。基数为0的集合称为空集。

**定义4.2：**集合$B$中的元素也是集合$A$的元素，则集合$B$是$A$的子集，表示为$B \subset A$；如果两个集合元素相同，则两个元素相等，即$B \subset A$且$A \subset B$，则$A=B$。

**定义4.3：**给定两个集合$A$和$B$，$B$在$A$中的补集为$\{ a \in A:a \notin B\} $，也可以表示为$A\backslash B$或者$A-B$，当$B \subset A$也可以表示成${B^C}$。

**定义4.4：**给定集合$A,B$，并集为$A \cup B$，代表$\{x:x \in A{\text{ or } }x \in B\}$，交集为$A \cap B$代表$\{x:x \in A{\text{ and } }x \in B\} $。

**定义4.5：**集合$A,B$的积用$A \times B$表示，代表：
$$
A \times B = \{(a,b):a \in A{\text{ and }}b \in B\}
$$

积是一种将实线$\mathbb{R}$转换为$\mathbb{R}^2$很好用的方式，定义${\mathbb{R}^2} = \mathbb{R} \times \mathbb{R}$，同理${\mathbb{R}^3} = \mathbb{R} \times \mathbb{R} \times \mathbb{R}$，这里可能会有点有疑惑，那就是$\mathbb{R}^3$如何展开，第一种可能性是：
$$
(\mathbb{R} \times \mathbb{R}) \times \mathbb{R} = \{ ((a,b),c):a \in \mathbb{R},b \in \mathbb{R},c \in \mathbb{R}\}
$$
第二种可能性是：
$$
\mathbb{R} \times (\mathbb{R} \times \mathbb{R}) = \{ (a,(b,c)):a \in \mathbb{R},b \in \mathbb{R},c \in \mathbb{R}\} 
$$
作为开发人员，很明显这两者是不同的，编译器会将上述两者认为是两种不同的东西，但作为数学家，出于某种原因，忽略了差异，认为两者是相同的，即：
$$
(\mathbb{R} \times \mathbb{R}) \times \mathbb{R} = \mathbb{R} \times (\mathbb{R} \times \mathbb{R}) = \{ (a,b,c):a \in \mathbb{R},b \in \mathbb{R},c \in \mathbb{R}\} 
$$
**定义4.6：**$A$和$B$是集合，$F$是$A \times B$的子集，如果$F$满足以下特性我们称它是一个函数：对任意$a \in A$都有唯一的$(a,b) \in F$；集合$A$称为$F$的域，集合$B$称为$F$的共域，用符号表示为：$f:A \to B$。

到目前为止，我们已经看到了许多定义的示例。实际上，我们将函数在计算上视为输入到输出的映射。下面举一个简单的例子：
$$
F = \{ (1,1),(2,4),(3,9),(4,16), \ldots \}  = \{ (x,{x^2}):x \in \mathbb{N}\}
$$
这个集合是$\mathbb{N} \times \mathbb{N}$的子集，现在我们可以对$(3,9) \in F$写下新的符号，使用映射的符号表示$F(3)=9$，这样，我们就可以按照我们想要的方式来描述$F$，即$F(x)=x^2$。通过定义4.6可以确保每个输入$x$都有某个输出$F(x)$，且只有一个输出$F(x)$。提供具体的算法来计算输出使得上述的条件微不足道，同时也不需要算法来定义函数。

至于为什么使用集合的术语来定义函数，部分是由于历史的原因，这里不对此做陈述，只需要知道集合是数学的基础即可。对于我们来讲，我们将函数看作与常规集合不同，函数具有语义上的输入输出依赖关系，我们将集合视作一种工具，用于帮助我们阐明概念或者消除一些定义中的歧义。现在，我们来看一下一些有关函数输入输出子集的有关定义。

**定义4.7：**给定函数$f:A \to B$，我们定义$f$的像为：
$$
f(A)=\{f(a):a \in A\}
$$

**定义4.8：**$A,B$是集合，$f:A \to B$是函数，有$b \in B$，$b$在$f$下的原像为${f^{ - 1}}(b)$，以集合形式表达为$\{a \in A: f(a)=b\}$。类似的，如果$C \subset B$是子集，则${f^{ - 1}}(C)$定义为$\{ a \in A: f(a) \in C\}$。

**定义4.9：**如果$a,a' \in A$不同，且$B$中的元素$f(a),f(a')$也不相同，则函数$f:A \to B$称为单射。

单射的示意图如下，是一种一一对应的关系：

![](/img/function_image.png)

**定义4.10：**如果对于任一$b \in B$，总有至少一个$a \in A$使得$f(a)=b$，这样的函数$f:A \to B$叫做满射；换句话说如果$f$的像为$B$，那么$f$是满射。

满射的示意图如下：

![](/img/surjection.png)

如果$f$既是单射又是满射，那么$f$就是双射，也叫做一一映射。仅双射存在逆。仅给出函数的描述来计算逆是非常困难的。实际上，大多数密码学都是基于这样的假设：某些函数在计算上不可逆；但另一方面，线性代数中计算矩阵的逆是可行的，因此，研究逆的概念也是有必要的。

**命题4.11：**逆是唯一的。

**证明：**假定$f:A \to B$是双射且${g_1}:B \to A$与${g_2}:B \to A$都是逆，假定$\forall b \in B$，有$f(a) = b$，则${g_1}(b) = {g_1}(f(a)) = a$，同理有${g_2}(b) = {g_2}(f(a)) = a$，则$g_1$与$g_2$相同。

**命题4.12：**假定$A,B$是集合，$f:A \to B$是双射，若$\forall a \in A$有$g(f(a)) = a$，$\forall b \in B$有$f(g(b)) = b$，则$g:B \to A$是$f$的逆。

现在稍微解释以下上文我们为什么视为$(\mathbb{R} \times \mathbb{R}) \times \mathbb{R} = \mathbb{R} \times (\mathbb{R} \times \mathbb{R})$，最根本的原因是存在双射$(\mathbb{R} \times \mathbb{R}) \times \mathbb{R} \to \mathbb{R} \times (\mathbb{R} \times \mathbb{R})$可以将$((a,b),c)$映射为$(a,(b,c))$。当数学家们想要称呼两个事物相同时，他们会想出这样的双射，认为双射两边应该被认为是相同的。

## 聪明的双射和计数

现在我们已经了解了关于集合的一些基本的描述语言，可以对一些问题进行建模了。假定现在想要计算集合的大小，由于集合可以隐式定义，可能不是那么容易计算。一种好用的方法是找到一种巧妙的双射，可以将看似困难的计数问题转变为优雅有技巧的问题。

来看第一个示例，假设你正在举办网球比赛，比赛是单淘汰赛，意味着两名选手结束比赛时，胜者留下，败者则退出比赛。作为比赛的主持人，你需要了解各种事情，比如完成比赛需要多长时间，要同时进行多少场比赛等等。要解决这些问题我们需要一个最基本的数据：一共有多少场比赛？也就是说给定由这个复杂的过程生成的比赛的集合，我们想要计算其大小。

假定我们有一千名选手，现在来探讨一下如何计算这一点。在第一轮，每个选手都会与其他选手配对，一共有500场比赛。第二轮中，剩下的500名选手再次配对参加比赛，一共有250场，在第三轮，有125场。在第四轮则会遇到问题，现在选手是奇数个了，那必然会出现选手轮空。好，现在比赛继续进行，最终会得到一个总数。这个答案是999，比选手的人数少1，这是巧合吗？对于别的比赛人数也是如此吗？

答案是肯定的，为了证明这一点，这里展示了找到巧妙双射的技巧。我们只需要观察到这样一个事实，每个选手都输掉一场比赛，所以如果我们要计算比赛次数，只需要计算失败选手的人数，只有一个没有失败的选手：胜利者，所以有999场比赛。

让我们把这个问题用集合的语言来描述，如果$X$是比赛的集合，而$Y$是选手的集合，我们可以定义这样一个函数$f:X \to Y$，称$f(x)$是关于失败者$x$的函数。$f(X)$的像是失败者的子集$L \subset Y$，实际上，$f$定义了关于$X$和$L$的双射，这意味着$X$和$L$有相同的大小。而$|L| = |Y| - 1$，所以有$n$个选手则有$n-1$场比赛。

为了确保理解这个过程，将示例扩展成双淘汰赛，即选手输了两场才会被淘汰。那么现在对任意的$y \in Y$有${f^{ - 1} }(y) = \{ x \in X:f(x) = y\} $的大小为2，胜利者有可能一场没输或者只输了一场，这种情况下肯定不是双射，那么就无法计算出确切的场数，但可以得到一个大概的边界。

这种常规的策略可以在你需要计数或者估计集合大小的时候使用。想象一下，你想估计城市中无家可归的人数，则必须找到一种巧妙的方法，通过观察他们的行为的残存的影响来隐式的对其计数，这恰恰是在要计算的集合接近双射或者双倍或三倍覆盖时寻找函数。

以下是找到巧妙双射的另一个例子。给定集合$X$，我们假定数量：

![](/img/4.1.png)

代表从$X$中选择2个，有如下的定义：

![](/img/4.2.png)

如果$X$是有限集，其大小为$n$，那么从这$n$个对象中挑选2个，很显然一共有$\frac{ {n(n - 1)} }{2}$种方式。接下来，我们将尝试用双射的方式来计算。图示如下：

![](/img/figure_4.4.png)

我们设置$n=7$，淡黄色的球为$Y$，最后一行$X$有$n$个方块。图示向我们展示了如何定义一个双射$g:Y \to C_X^2$，很显然，我们能从图中得到答案$1 + 2 +  \cdots  + (n - 1)$。

## 归纳和矛盾证明

接下来我们会接触两种严格的证明方法，一种是归纳法，也就是递归。我们是这样理解递归的：函数能够以更小的参数集来调用自身，并以基本情况来处理允许的最小参数，经典的例子是斐波那契数列：
$$
fib(n) = fib(n - 1) + fib(n - 2)
$$
同时$fib(0) = fib(1) = 1$。

与其相似，归纳法是一种证明方法，当要证明一个命题时，允许使用最基本的情况、更简单的参数来使用这个命题最终达到证明这个命题的目的。困难在于何时何地使用归纳法，通常是在证明所有自然数适用的命题时，例如：对于所有整数$n \geqslant 6$都有$P(n)$为true。归纳证明分两步进行：

1. 首先列出最基本的情况，对于此例来说是$P(6)$为true。
2. 之后是归纳步骤，使用$P(n)$为true来证明$P(n+1)$为true，同理，也可以使用$P(n-1)$来证明$P(n)$。

像递归一样，我们可以得到一连串的证明：$P(6)$隐含着$P(7)$为true，一直到$P(n)$。

现在我们利用归纳法来证明：

![](\img\4.3.png)

先从最基本的情况开始，由于$n \geqslant 2$，当$n$为2时，答案为1，成立。另外，如果：

![](\img\4.4.png)

则必有：

![](\img\4.5.png)

假设集合$X = \{ 1,2, \ldots ,n + 1\} $，现在将其分成两部分，一部分是两个元素都从$Y = X - \{ n + 1\}  = \{ 1,2, \ldots ,n\} $中选择。另一部分则是取的两个元素有一个是$n+1$，显然，两部分加起来就是我们要证明的问题。

第一部分，有：

![](\img\4.6.png)

答案应为命题假设所述$1 + 2 +  \cdots  + n - 1$。

第二部分更为简单，我们取的方法只有$n$种。合在一起，一共有$1 + 2 +  \cdots  + n$种，命题得证。有趣的是，归纳证明在数学上的声誉很差，因为其往往不能向读者传达任何见识，我们对上述的证明也不如使用图像示意来得直观。

第二种证明的方法是矛盾证明，有如下的例子：你正在参加派对，出于好奇，你问你的朋友他在聚会上有几个朋友，他数了数一共有五个。同时，你也数了数发现自己也有五个朋友。真是巧合，现在你处于数学家的敏锐洞察力觉得这可能有深层的原因，于是你调查了一番，发现其他人在聚会上也有五个朋友。那么，每个聚会都是这样吗？聚会上是否总会有至少两个人有相同数量的朋友？答案是肯定的。

证明如下：假设有聚会每个人都有不同数目的朋友，假设聚会总共有$n$个人，每个人的朋友数目在0和$n-1$之间，这是一个闭区间。由于有$n$个人，而且有$n$个不相等的数字，其属于$[0,n-1]$。我们可以将每个人映射到其所拥有的朋友数量，并且该映射是双射。现在就出现了一个矛盾，有人必须有0个朋友，而有人必须有$n-1$个朋友，这意味着他必须是所有人的朋友，这显然矛盾，因此假设不成立。

使用矛盾进行证明的目的是使对象具有某种可以使用的属性，如果你试图证明不存在具有某些特殊属性的对象，你可以通过矛盾证明假设这种对象存在，使用特殊属性继续进行证明。

## 应用：稳定的婚姻

问题如下：现在有$n$位男性和女性，最终的目标是选择谁应该嫁给谁，如果我们将$M$称为男性，$W$称为女性，我们的目的是找到双射$M \to W$来描述婚姻。

给出以下稳定的定义：

**定义4.13：**双射$f:M \to W$稳定，意味着没有成对的$m \in M$与$w \in W$满足以下两个条件：

1. $f(m) \ne w$，意味着两者不匹配。
2. 比起他们分配的对象，成对者更喜欢对方，即$ran{k_m}(w) < ran{k_m}(f(m))$和$ran{k_w}(m) < ran{k_w}({f^{ - 1}}(w))$。

现在，算法问题是给定男女双方的偏好列表作为输入，我们是否可以找到稳定的婚姻？我们可以保证对任何一个偏好表稳定的婚姻都存在吗？答案都是肯定的，这使用了延迟接受的算法。

这是算法的非正式描述：轮流进行，在每轮中，每个男性都向尚未拒绝他的自己最喜欢的女性求婚，另一方面，女性如果在本轮中被求婚，她会拒绝每个求婚人，不过她最喜欢的除外，但她也不会接受，会推迟到最后接受。最拒绝的男性很伤心，但他们在下一轮会继续向下一个喜欢的女性求婚。到了最后，没有人会剩下，这些女性的选择会构成一个稳定的双射。

用程序表示如下，suitors向suiteds求婚：

```python
class Suitor:
    def __init__(self, id, preference_list):
        """ A Suitor consists of an integer id (between 0 and the total number
        of Suitors), and a preference list implicitly defining a ranking of the
        set of Suiteds.

        E.g., Suitor(2, [5, 0, 3, 4, 1, 2]) says the third Suitor prefers the
        Suited with index 5 the most, then the Suited with index 0, etc.

        The Suitor will propose in decreasing order of preference, and maintains
        the internal state index_to_propose_to to keep track of the next proposal.
        """
        self.preference_list = preference_list
        self.index_to_propose_to = 0
        self.id = id

    def preference(self):
        return self.preference_list[self.index_to_propose_to]

    def post_rejection(self):
        self.index_to_propose_to += 1

    def __eq__(self, other):
        return isinstance(other, Suitor) and self.id == other.id

    def __hash__(self):
        return hash(self.id)

    def __repr__(self):
        return "Suitor({})".format(self.id)
   
class Suited:
    def __init__(self, id, preference_list):
        self.preference_list = preference_list
        self.held = None
        self.current_suitors = set()
        self.id = id

    def reject(self):
        """Return the subset of Suitors in self.current_suitors to reject,
        leaving only the held Suitor in self.current_suitors.
        """
        if len(self.current_suitors) == 0:
            return set()

        self.held = min(self.current_suitors,
                        key=lambda suitor: self.preference_list.index(suitor.id))
        rejected = self.current_suitors - set([self.held])
        self.current_suitors = set([self.held])

        return rejected

    def add_suitor(self, suitor):
        self.current_suitors.add(suitor)

    def __eq__(self, other):
        return isinstance(other, Suited) and self.id == other.id

    def __hash__(self):
        return hash(self.id)

    def __repr__(self):
        return "Suited({})".format(self.id)
```

以下是延迟接受算法的主要代码：

```python
def stable_marriage(suitors, suiteds):
    """ Construct a stable marriage between Suitors and Suiteds.

    Arguments:
        suitors: a list of Suitor
        suiteds: a list of Suited, which deferred acceptance of Suitors.

    Returns:
        A dict {Suitor: Suited} matching Suitors to Suiteds.
    """
    unassigned = set(suitors)

    while len(unassigned) > 0:
        for suitor in unassigned:
            next_to_propose_to = suiteds[suitor.preference()]
            next_to_propose_to.add_suitor(suitor)
        unassigned = set()

        for suited in suiteds:
            unassigned |= suited.reject()

        for suitor in unassigned:
            suitor.post_rejection()  # have some ice cream

    return dict([(suited.held, suited) for suited in suiteds])
```

**定理4.14：**延迟接受算法总是能够终止，并且最终能够产生稳定的双射。

证明这里不再赘述，可以参见对应章节。