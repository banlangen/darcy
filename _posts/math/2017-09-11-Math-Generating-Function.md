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

&emsp;&emsp;解释下这段描述。在数学中为了研究一个无限序列{$$a_n$$}，于是将这个序列的每一个元素对应为一个多项式中的系数，这个多项式就是我们现在讨论的生成函数。为什么这么做？我的粗浅理解是想通过多项式对这个序列的行为进行模拟，使得对序列的讨论可以转换到对多项式的讨论，如果你还记得微积分的话，你应该会知道泰勒展开式，泰勒展开式其实就是使用多项式对一个函数进行逼近，从而将对这个函数的问题的讨论转换到对多项式的讨论上，生成函数应该也带有同样的意味。那为什么选择多项式而不是其他的东东进行逼近？这是因为多项式是当时人们理解研究最深入的一个领域，这么做其实也是对问题化繁为简（或者说再次抽象）的一个手段。我们可以看到在后面讨论数学中的一个神奇序列Catalan Number的时候，我们只有通过生成函数，才能得到符合数理逻辑的代数证明（这种证明抛开了问题所处的上下文环境，是一个纯粹的符号和代数角度的更通用的证明）。如果没有生成函数，我们只能结合具体问题给出几何上的具体分析，这并非是一个“放之四海皆准”的证明方法。

&emsp;&emsp;英文描述中还提到一个重要的事实，生成函数是允许发散的，这是跟泰勒展开式的一个重要区别，泰勒展开式既然是用多项式进行逼近的，所以该多项式必须是收敛的，也就是说只有这个多项式的余项是个高阶无穷小，那么泰勒展开式才是成立的，生成函数没有这个要求，这也是可以理解的，毕竟生成函数是离散数学领域的概念，都不连续何谈收敛？

#### Another way of counting

&emsp;&emsp;你可能会问生成函数到底可以用来干什么？我们生活中用的到生成函数吗？  
&emsp;&emsp;肯定是用的到的，而且他的应用领域是如此的贴近生活，完全不像他的名称那样给人一种距离感。如果你已经看了本博客的另一篇文章[Binomial Theorem](http://blog.marvingalaxy.info/2017/09/10/Math-Binomial-Theorem/)你肯定会惊叹于二项式系数与组合之间的天然联系，而二项式是只有两项的多项式，它其实是多项式的一种特殊形式，所以二项式系数与组合之间的联系其实是继承于多项式的，我们看几个例子，帮助你理解其中的含义。

>假设你面前放着一个水果篮，里面有一个梨，一个苹果，一个橙子，一把香蕉和一个木瓜，而你只能从中挑选两样水果，请问你有多少种挑选的方法？

&emsp;&emsp;这是一个非常简单的组合问题，那么按照组合概念，一共有$${C_2^5}^{[注1]} = \frac{5!}{2!3!} = 10$$种选择的方法。那如果我们要用生成函数来“逼近”这个问题呢？我们先别在意只能选两个水果这个条件，抛开这点约束，假设我不定要选几个水果出来，可以只选几个，也可以全选，当然也可以全不选，这样的话，水果的所有选择方法用组合公式表示就是$${C_0^5 + C_1^5 + C_2^5 + C_3^5 + C_4^5 + C_5^5 = 32}^{[注1]}$$种。换个思路我们也可以将这个问题理解为5个水果，每个都有两种选择方案，0个或者1个，那就一共有$${C_1^2 \cdot C_1^2 \cdot C_1^2 \cdot C_1^2 \cdot C_1^2 = 32}^{[注1]}$$种方案，这种思路可以用下图表示，同时在这个基础上我们尝试用二项式进行替换，替换的原则是用变量x代表水果，x的指数代表选择的个数，于是可以得到如下的对应关系  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;$$\binom{0\;pear \quad 1\;pear}{x^0 \quad + \quad x^1} \cdot \binom{0\;apple \quad 1\;apple}{x^0 \quad + \quad x^1} \cdot \binom{0\;orange \quad 1\;orange}{x^0 \quad + \quad x^1} \cdot \binom{0\;banana \quad 1\;banana}{x^0 \quad + \quad x^1} \cdot \binom{0\;papaya \quad 1\;papaya}{x^0 \quad + \quad x^1}$$  
式子中我们用“+”来代表“或”的概念，所以就转变成5个二项式相乘$$(x^0 + x^1)(x^0 + x^1)(x^0 + x^1)(x^0 + x^1)(x^0 + x^1)$$，$$x^0 = 1$$，所以进一步简化为$$(1 + x)^5 = 1 + 5x + 10x^2 + 10x^3 + 5x^4 + x^5$$，其中$$x^2$$的系数正好是10，如果你已经理解了[Binomial Theorem](http://blog.marvingalaxy.info/2017/09/10/Math-Binomial-Theorem/)，自然你对下面这个公式不会感到陌生，这其实就根据二项式定理进行展开，所以其系数告诉了我们准确的答案。  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;$$(1 + x)^5 = C_0^5 + C_1^5x^1 + C_2^5x^2 + C_3^5x^3 + C_4^5x^4 + C_5^5x^5$$  
而$$C_0^5 + C_1^5x^1 + C_2^5x^2 + C_3^5x^3 + C_4^5x^4 + C_5^5x^5$$就是我们的生成函数。

>在前面问题的基础上，假设将篮子中的香蕉换成苹果，于是篮中便有两个苹果（可以认为这两个苹果完全一样），没了香蕉，其他水果个数保持不变，还是从中挑选两样水果，请问有多少种挑选的方法？

&emsp;&emsp;这个问题用组合可就没有那么容易解答了，相对的，如果用生成函数，解答就会更容易理解和直观，对于苹果而言我们有三种选择方式，用多项式表达就是$$(x^0 + x^1 + x^2)$$，而其他的水果的选择方式不变，可以用二项式表达$$(x^0 + x^1)$$，所以这个问题的生成函数可以用$$(x^0 + x^1 + x^2)(x^0 + x^1)^3$$展开得到，于是有了$$(1 + x + x^2)(1 + x)^3 = 1 + 4x + 7x^2 + 7x^3 + 4x^4 + x^5$$，$$x^2$$的系数是7，所以一共有7种方法，为了说明这个答案的正确性，我们直接通过暴力方法进行核对。
$$\begin{array}{|c|c|}
\hline
1&2 \\
\hline
3&4 \\
\hline
\end{array}$$

#### Comments

- [注1]：中国大陆的教科书里面将组合（排列也是如此）的n中取k的情况标记为$$C_n^k$$，这与国际上的标注法是相反的，此处采用的是国际标注法。同时还需要注意的是排列的标记在国际上是P取自英文permutation，中国大陆的教科书中用的标记是A。此博客完全使用国际标注法。