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

>假设你面前放着一个水果篮，里面有一个梨，一个苹果，一个橙子，一把香蕉和一个木瓜，而你只能从中挑选两样，请问你有多少种挑选的方法？

&emsp;&emsp;这是一个非常简单的组合问题，那么按照组合概念，一共有$${C_2^5}^{[注1]} = \frac{5!}{2!3!} = 10$$种选择的方法。那如果我们要用生成函数来“逼近”这个问题呢？
（请原谅我下面用X^1代表x的1次方，图片中插入数学公式非常麻烦，这种事儿上我特别喜欢偷懒。）我们先别在意只能选两个水果这个条件，抛开这点约束，假设我不定要选几个水果出来，可以只选几个，也可以全选，当然也可以全不选，这样的话，我们就知道这样的选择方法用组合公式表示的话，就是$${C_0^5 + C_1^5 + C_2^5 + C_3^5 + C_4^5 + C_5^5 = 32}^{[注1]}$$种
![math01](http://ovwkcbdpf.bkt.clouddn.com/image/math/math_01.png '生成函数逼近')   


#### Comments

- [注1]：中国大陆的教科书里面将组合（排列也是如此）的n中取k的情况标记为$$C_n^k$$，这与国际上的标注法是相反的，此处采用的是国际标注法。同时还需要注意的是排列的标记在国际上是P取自英文permutation，中国大陆的教科书中用的标记是A。此博客完全使用国际标注法。