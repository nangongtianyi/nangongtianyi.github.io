---
title: Programmer and Mathematics (一)
date: 2021-01-09 13:24:25
categories:
    - 文章
mathjax: true
---

# 多项式

从加密开始，假设现在有一条秘密消息，将其分成10个部分进行编码，接收方只要知道任意6个部分，就可以重建消息，但如果少于6个部分，甚至不能确定原始消息的一小段，要实现这种方案，多项式足以。

<!-- more -->

**定理2.1：**实系数单变量多项式是输入为实数输出也为实数的一种函数，形式如下：
$$
f(x) = {a_0} + {a_1}x + {a_2}{x^2} + ... + {a_n}{x^n}
$$

其中${a_i}$是$f(x)$的系数，且必须是非负整数，多项式的次数为$n$。

从程序语言来讲，一个关于系数的数组就可以限定一个多项式，例如a[i]就代表${a_i}$，数组的长度就代表多项式的次数。

多项式是非常重要的，其内部的乘加特性，可以延申到所有的算数运算。现在暂时扩展到多变量，在程序语言中的与或非，就是非常简单的多变量多项式，但最终能产生全部的算法范围。

考虑一种特殊情况，虽然次数存在，但系数全部为0。在这种情况下，虽然是合理的但次数就失去了其应有的意义，因此，“按惯例”，最后一个系数${a_n}$应该是非零的，同时，特别定义$f(x) = 0$是零多项式，其次数为-1。

当定义一个函数的时候通常使用如下的表示：$f:A \to B$。所有可能的输入被称作域，所有可能的输出被称作范围。在数学中，范围是所有真实输出的集合，输出的类型称为共域。在上述的表达中，我们指定$A$代表域，$B$代表共域。

了解了一些基本的概念之后，可以着手实现前文所述的加密，这里需要利用到以下的定理：经过给定点集的多项式的存在性与唯一性定理。

**定理2.2：**对任意整数$n \ge 0$和属于$\mathbb{R}^{2}$的$n+1$个点的点集$({x_0},{y_0}),({x_1},{y_1}),...,({x_n},{y_n})$，其中${x_0} < {x_1} < {x_2} < ... < {x_n}$，存在一个唯一的$n$次多项式，使得对所有的$i$有$p({x_i}) = {y_i}$。

其中，$\mathbb{R}^{2}$代表了一对实数，每个实数都属于$\mathbb{R}$，类似的，$\mathbb{Z}^{3}$代表一个整数的三元组。

这个定理可以用一种更简短的方式陈述：存在唯一的$n$次多项式，其经过了$n+1$个点的选择。当看见一个新定理的时候，要做的第一件事就是写下一个最简单的例子，这样除了能够简化定理，还能够提供示例，为审阅证明定理的时候使用。例如对以上的定理选择$(7,4)$这个例子，这是一个零次多项式，函数唯一且确定，为$f(x)=4$。接下来稍微复杂一点，考虑数据为$(2,3),(7,4)$，这是一个一次多项式，也能很容易的确定这个多项式应为$f(x) = \frac{ {13} } {5} + \frac{1} {5}x$。在几何上，次数为1的多项式是一条直线。这是显而易见的，在两点之间有唯一的一条直线。此外，定理还指出了${x_0} < {x_1} < {x_2} < ... < {x_n}$，那么来考虑下${x_0} = {x_1}$的情况，例如$(2,3),(2,5)$。

我们不考虑真实答案，只猜测可能没有次数为1的多项式经过这两点，或者有多个次数为1的多项式经过这两点，那么就破坏了唯一性。因此，我们应该尝试以一种更加精确的方式阅读定义。

现在考虑证明2.2，将包括两个部分，存在性和唯一性。首先，我们将证明存在一个满足要求的多项式，然后证明如果两个多项式都满足要求，则它们必须相同。下面将通过直接构造的方式来证明存在性。与前文类似，我们还是从最简单的方式开始，但是是以一种通用的形式。此时如果是一个点$(x_1, y_1)$，则多项式为$f(x) = {y_1}$，两个点的情况我们直接写成以下的形式$f(x) = {y_1}\frac{ {x - {x_2} } } { { {x_1} - {x_2} } } + {y_2}\frac{ {x - {x_1} } } { { {x_2} - {x_1} } }$，显然，满足要求，且式中已经包含了${x_1} \ne {x_2}$。将其简化为多项式的标准形式：
$$
f(x) = \frac{ { {x_1} {y_2} - {x_2} {y_1} } } { { {x_1} - {x_2} } } + (\frac{ { {y_1} - {y_2} } } { { {x_1} - {x_2} } })x
$$
显然，$x$的幂没有出现大于1的情况，而且没有出现两个$x$相乘的情况，那么，可以确信此多项式的次数为1.

三个点的多项式，我们也可以按照以上的方式进行构造：
$$
f(x) = {y_1}\frac{ {(x - {x_2})(x - {x_3})} } { {({x_1} - {x_2})({x_1} - {x_3})}  } + {y_2}\frac{ {(x - {x_1})(x - {x_3})} } { {({x_2} - {x_1})({x_2} - {x_3})} } + {y_3}\frac{ {(x - {x_1})(x - {x_2})} } { {({x_3} - {x_1})({x_3} - {x_2})} }
$$
同理，$n+1$个点的多项式就很容易构造了，如下：
$$
f(x) = \sum\limits_{i = 0}^n { {y_i}(\prod\limits_{j \ne i} {\frac{ {x - {x_j} } } { { {x_i} - {x_j} } } } )}
$$
此时，其实已然证明了存在性，因为每一项都是$n$次的，这显然是一个$n$次的多项式。

下面展示以下上式中某些数学符号的代码展示，有以下的例子：
$$
f(x) = \sum\limits_{i = 0}^n {bar(i)(\prod\limits_{j \ne i} {foo(i,j)} )}
$$

```c++
int i, j;
sometype theSum = defaultSumValue;
for (i = 0; i <= n; i++) {
	othertype product = defaultProductValue;
	for (j = 0; j <= n; j++) {
		if (j != i) {
			product *= foo(i, j);
		}
	}
	theSum += bar(i) * product;
}
return theSum;
```

下面证明唯一性，依赖如下定理：

**定理2.3：**零多项式是实数内唯一一个次数最多为$n$，但有超过$n$个不同根的多项式。

现在来进行证明，假设有两个$n$次的多项式，经过点集$({x_0},{y_0}),({x_1},{y_1}),...,({x_n},{y_n})$，这两个多项式可以相同也可以不同，我们所要做的是证明这两个多项式必须相同，那么就证明了唯一性。现在构造这样一个多项式$(f - g)(x)$，定义$(f - g)(x) = f(x) - g(x)$，如果$f$的系数为$a_i$，$g$的系数为$b_i$，那么$f-g$的系数为$c_i=a_i-b_i$，显然$f-g$是一个多项式。我们对这个多项式了解多少呢，首先，这个多项式的次数最多是$n$，而且我们知道$(f - g)({x_i}) = 0$。现在我们使用定义2.3，我们假定$f-g$的次数为$d \leqslant n$，我们知道此多项式的根不超过$n$个，除非它是零多项式，但有$n+1$个点（即上文所述点集中的点）可以使上式成立，因此这是一个零多项式，因此$f$跟$g$相同。

既然已经通过给定点集证明了$n$次多项式的存在性和唯一性，那么就可以为其命名，成为给定点的插值多项式，插值意味着获取点集，并找到通过这些点的唯一最小次多项式。

## 代码实现

以下将编写一个插值点的python程序，将假设存在一个多项式类，该类接受一系列参数并生成多项式，如下：

```
def interpolate(points):
    """Return the unique polynomial of degree at most n passing through the given n+1 points."""
    if len(points) == 0:
        raise ValueError('Must provide at least one point.')

    x_values = [p[0] for p in points]
    if len(set(x_values)) < len(x_values):
        raise ValueError('Not all x values are distinct.')

    terms = [single_term(points, i) for i in range(0, len(points))]
    return sum(terms, ZERO)
```

输入点集后，通过single_term函数生成单项，将这些单项相加即是多项式，生成单项的代码如下：

```
def single_term(points, i):
    """Return one term of an interpolated polynomial.

    This method computes one term of the sum from the proof of Theorem 2.2.
    In particular, it computes:

      y_i \product_{j=0}^n (x - x_i) / (x_i - x_j)

    The encapsulating `interpolate` function sums these terms to construct
    the final interpolated polynomial.

    Arguments:
      - points: a list of (float, float)
      - i: an integer indexing a specific point

    Returns:
      A Polynomial instance containing the desired product.
    """
    the_term = Polynomial([1.])
    xi, yi = points[i]

    for j, p in enumerate(points):
        if j == i:
            continue

        xj = p[0]

        """
        The inlined Polynomial instance below is how we represent

          (x - x_i) / (x_i - x_j)

        using our Polynomial data type (where t is the variable, and
        x_i, x_j are two x-values of data points):

          (x - x_i) / (x_i - x_j) = (-x_j / (x_i - x_j)) * t^0
                                  +    (1 / (x_i - x_j)) * t^1
        """
        the_term = the_term * Polynomial([-xj / (xi - xj), 1.0 / (xi - xj)])

    # Polynomial([yi]) is a constant polynomial, i.e., we're scaling the_term
    # by a constant.
    return the_term * Polynomial([yi])
```

这里利用了上文所述的构造方法，每一项为${y_i}(x - {x_j})/({x_i} - {x_j})$，这里将其分解成了${a_0} =  - {x_j}/({x_i} - {x_j})$和${a_1} = 1/({x_i} - {x_j})$来生成一个简单的多项式。

## 实践

以下将使用多项式插值来实现加密。假设武林盟主有五个得力手下，他向他们分享一个秘密，秘密以二进制表示，也许这个秘密是一张藏宝图。问题在于这些手下是贪婪的，如果直接把秘密给他们，或许有人会直接独吞藏宝图；如果只给一部分，他们也有可能直接找到藏宝图，更糟糕的是，如果三个人聚在一起，很可能会猜中剩余的部分，排除掉另外两人。因此，为了安全，这个秘密应该具有以下的属性：

1. 每个人只有获得了部分秘密，且这部分是独一无二的；
2. 如果任意四个人聚在一起共享秘密，他们也不能得到完整的秘密；
3. 如果五个人全部聚在一起，他们才能得到完整的秘密，拿到藏宝图。

实际上，任意四个人聚在一起不只是不能获取完整的秘密，他们甚至破译不出任何秘密。神奇的是是有这种方案的，无论有多少个人（$n$），或者是希望有多少组（$k$）能重建秘密，这都是可能的。以下给出这种方案，即使用多项式插值。我们将秘密用整数$s$表示，有$f(0)=s$，现在我们想让五个手下齐聚能得到秘密，因此$k$就是5，那么我们要构造的多项式的次数就是$k-1$也就是4，系数随机生成即可，然后将$f(1),f(2),f(3),f(4),f(5)$分发作为秘密的部分分发给手下，这样，只有五个人齐聚才能拿到藏宝图。