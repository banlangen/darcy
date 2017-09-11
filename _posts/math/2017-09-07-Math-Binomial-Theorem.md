---
layout: post
title: "Binomial Theorem"
date: 2017-09-10 19:00:00 +0800 
categories: 
    - Mathematics 
    - Algebra
tags: 
comments: true
---
* content
{:toc}

二项式定理描述了二项式的幂的代数展开，其中的二项式系数（Binomial Coefficient）更是应用广泛，本文原创，转载请标明出处。

<!-- more -->

## Binomial Theorem

#### Description

>[二项式定理（Binomial Theorem）:](https://zh.wikipedia.org/wiki/%E4%BA%8C%E9%A1%B9%E5%BC%8F%E5%AE%9A%E7%90%86 "wikipedia") 在初等代数中，二项式定理描述了二项式的幂的代数展开。根据该定理，可以将两个数之和的整数次幂诸如 $$(x + y) ^ n$$ 展开为类似于 $$ax^by^c$$ 项之和的恒等式，其中b、c均为非负整数而且b + c = n，系数a是依赖于n和b的正整数（或者n和c），也被称为二项式系数，记为 $$\binom{n}{b}$$ 或者 $$\binom{n}{c}$$（两者值相等）。  

#### Threorem statement

>根据此定理，可以将x + y的任意次幂展开成和的形式  
$$(x + y) ^ n = \binom{n}{0}x^ny^0 + \binom{n}{1}x^{n-1}y^1 + \binom{n}{2}x^{n-2}y^2 + \cdot\cdot\cdot + \binom{n}{k}x^{n-k}y^k + \cdot\cdot\cdot + \binom{n}{n-1}x^1y^{n-1} + \binom{n}{n}x^0y^n$$  
其中每个$$\binom{n}{k}$$为一个称作**二项式系数**的特定正整数，其含义是从n个元素中挑选k个元素的方法数，与组合$${C_k^n}^{[注1]}$$的含义是相同的，其值等于$$\frac{n!}{k!(n-k)!}$$。这个公式也被称作**二项式公式**或**二项恒等式**。使用求和符号可以写作  
$$(x + y) ^ n = \sum\limits_{k=0}^n\binom{n}{k}x^{n-k}y^k = \sum\limits_{k=0}^n{\binom{n}{k}}x^ky^{n-k}$$  

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