---
layout: post
title: "Ordinary Generating Function"
date: 2017-09-11 19:00:00 +0800 
category: 数学
tags: 
     - Discrete Mathematics
---
* content
{:toc}

生成函数（Generating Function）是离散数学（Discrete Mathematics）中的一个内容，而计算机科学的数据基础是离散数学，同时由于计算机科学的迅猛发展，离散数学的概念得以广泛应用于日常生活中，两者相辅相成。这个地方我们讨论生成函数中的一种普通生成函数（Ordinary Generating Function），目的是为后面讨论Catalan Number做一个铺垫，从探讨过程中可以看到计算机编程如何将离散数学的一些基本知识应用到具体的生活实践中。

<!-- more -->

## Generating Function

#### Description

>[生成函数(Generating Function)](https://en.wikipedia.org/wiki/Generating_function), 定义如下：  
&emsp;&emsp;In mathematics, the term generating function is used to describe an infinite sequence of numbers $$(a_n)$$ by treating them as the coefficients of a series expansion. The sum of this infinite series is the generating function. Unlike an ordinary series, this formal series is allowed to diverge, meaning that the generating function is not always a true function and the "variable" is actually an indeterminate. 

解释下这段英文描述。在数学中为了研究一个无限序列{$$a_n$$}，于是将这个序列的每一个元素对应带一个多项式里面的系数，这个多项式就是我们现在讨论的生成函数，为什么这么做？我的粗浅理解是想通过多项式对这个序列的行为进行逼近，使得对序列的讨论可以转换到对多项式的讨论，如果你还记得微积分的话，你应该会知道泰勒展开式，泰勒展开式其实就是使用多项式对一个函数进行逼近，从而将对这个函数的问题的讨论转换到对多项式的讨论上，生成函数应该也带有同样的意味。那为什么选择多项式而不是其他的东东进行逼近？这是因为多项式是当时人们理解研究最深入的一个领域，这么做其实也是对问题化繁为简（或者说再次抽象）的一个手段。我们可以看到在后面讨论数学中的一个神奇序列Catalan Number的时候，我们只有通过生成函数，才能得到符合数理逻辑的代数证明（这种证明抛开了问题所处的上下文环境，是一个纯粹的符号和代数角度的更通用的证明）。如果没有生成函数，我们只能结合具体问题给出几何上的具体分析，这并是一个“放之四海皆准”的证明方法。

英文描述中还提到一个重要的事实，生成函数是允许发散的，这是跟泰勒展开式的一个重要区别，泰勒展开式既然是用多项式进行逼近的，所以该多项式必须是收敛的，也就是说只有这个多项式的余项是个高阶无穷小，那么泰勒展开式才是成立的，生成函数没有这个要求，这也是可以理解的，毕竟生成函数是离散数学领域的概念，都不连续何谈收敛？

#### Another way of counting

&emsp;&emsp;你可能会问生成函数到底可以用来干什么？我们生活中用的到生成函数吗？  
&emsp;&emsp;肯定是用的到的，而且他的应用领域是如此的贴近生活，完全不像他的名称那样给人一种距离感。 
&emsp;&emsp;如果你已经看了本博客的另一篇文章[Binomial Theorem](http://blog.marvingalaxy.info/2017/09/10/Math-Binomial-Theorem/)你肯定会惊叹于二项式系数与组合之间的天然联系，而二项式是只有两项的多项式，它其实是多项式的一种特殊形式，所以二项式系数与组合之间的联系其实是继承于多项式的，我们看几个例子，帮助你理解其中的含义。



#### Explanation

&emsp;&emsp;现在我们用示例来说明以上公式的含义与使用规则。

&emsp;&emsp;首先需要说明的是$${C_k^n}^{[注1]} = \binom{n}{k}$$，也就是二项式系数其实是一个组合。但为何二项式系数和组合有关系？这是可以通过数学归纳法来证明的，这个地方我并不想展开，因为我们其实完全没有必要知道这个关系的数学证明过程，我们只需要知道应该如何理解这个关系。  
&emsp;&emsp;大家肯定都知道$$(x + y)^2$$应该如何计算，我们有公式$$(x + y)^2 = x^2 + 2xy + y^2$$，其中的2xy是由于$$(x + y)(x + y)$$的展开过程中产生了1个xy，和1个yx，xy和yx是相同的，所以合并之后就变成了2xy，展开过程如下:  
&emsp;&emsp;$$(x + y)(x + y) = x^2 + xy + yx + y^2$$  
&emsp;&emsp;那如果是$$(x + y)^3$$呢?  
&emsp;&emsp;$$(x + y)(x + y)(x + y) = xxx + {\color{red}{xxy + xyx + yxx}} + yyx + yxy + xyy + yyy$$  
&emsp;&emsp;红色部分一共有3个，写成幂形式也就是$$3(x^2y)$$，为了方便说明这里特意不用幂表示。现在我们用组合的概念来思考红色部分是如何形成的，首先对原恒等式的左边进行标注$$(x + y)_{(a)}(x + y)_{(b)}(x + y)_{(c)}$$其中的$$(a), (b), (c)$$是为了说明方便，没有任何数学含义，所以等式左边可以理解为三个$$(x + y)$$的乘积，他们的下标分别为$$(a), (b), (c)$$，二项式展开的过程可以理解为这样一个过程，为了得到结果我们要从$$(x + y)_{(a)}$$里面挑一项(x或者y)出来，乘以$$(x + y)_{(b)}$$中挑一项出来，再乘以$$(x + y)_{(c)}$$中挑一项出来。如果只关注$$(x^2y)$$，那么就一共要挑两个x和一个y。三个$$(x + y)$$中挑两个x出来（剩下的那个肯定就是挑y），等价于从三个盒子里面挑两个盒子出来存放x，那挑选的方法就有$${C_2^3}^{[注1]}$$种，所以$$(x^2y)$$的系数就是3。同理如果我们关注$$x^3$$的系数，那就是$$(x + y)_{(a)}$$, $$(x + y)_{(b)}$$, $$(x + y)_{(c)}$$中每个都取x，也就是三个盒子中取出三个来存放x，有$$C_3^3 = 1$$种取法，所以$$(x^3)$$项的系数就是1。  
&emsp;&emsp;现在我们延伸到n次方的情形，考虑$$(x + y)^n$$，相当于$$(x + y)(x + y)\cdot\cdot\cdot(x + y)$$一共有n项$$(x + y)$$相乘，现在要求$$x^ky^{n-k}$$的系数，也就是n个$$(x + y)$$中挑选k个x出来，那么最后的答案就是$${C_k^n}^{[注1]} = \frac{n!}{k!(n-k)!}$$。

&emsp;&emsp;接着需要理解x和y的指数的加和是n，这个用组合的方法也很好解释，n个$$(x + y)$$中要进行n次挑选，每次挑选不是选x就是选y，自然最后就有k个x和n-k个y。  
&emsp;&emsp;所以最后我们就可以得到这样的公式：  
&emsp;&emsp;$$(x + y) ^ n = \binom{n}{0}x^0y^n + \binom{n}{1}x^{1}y^{n-1} + \binom{n}{2}x^{2}y^{n-2} + \cdot\cdot\cdot + \binom{n}{k}x^{k}y^{n-k} + \cdot\cdot\cdot + \binom{n}{n-1}x^{n-1}y^1 + \binom{n}{n}x^ny^0$$  
&emsp;&emsp;但是更习惯的我们会交换下x和y的指数，写成如下的等价形式：  
&emsp;&emsp;$$(x + y) ^ n = \binom{n}{0}x^ny^0 + \binom{n}{1}x^{n-1}y^1 + \binom{n}{2}x^{n-2}y^2 + \cdot\cdot\cdot + \binom{n}{k}x^{n-k}y^k + \cdot\cdot\cdot + \binom{n}{n-1}x^1y^{n-1} + \binom{n}{n}x^0y^n$$

#### Comments

- [注1]：中国大陆的教科书里面将组合（排列也是如此）的n中取k的情况标记为$$C_n^k$$，这与国际上的标注法是相反的，此处采用的是国际标注法。同时还需要注意的是排列的标记在国际上是P取自英文permutation，中国大陆的教科书中用的标记是A。此博客完全使用国际标注法。