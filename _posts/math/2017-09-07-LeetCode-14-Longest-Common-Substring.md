---
layout: post
title: "Binomial theorem"
date: 2017-09-10 19:00:00 +0800 
categories: 
    - Mathematics 
    - Algebra
tags: 
---
* content
{:toc}

二项式定理描述了二项式的幂的代数展开，其中的二项式系数（Binomial Coefficient）更是应用广泛。

<!-- more -->

## Binomial theorem

#### Description

>[二项式定理:](https://zh.wikipedia.org/wiki/%E4%BA%8C%E9%A1%B9%E5%BC%8F%E5%AE%9A%E7%90%86 "wikipedia") 在初等代数中，二项式定理（Binomial theorem）描述了二项式的幂的代数展开。根据该定理，可以将两个数之和的整数次幂诸如 $$(x + y) ^ n$$ 展开为类似于 $$ax^by^c$$ 项之和的恒等式，其中b、c均为非负整数而且b + c = n，系数a是依赖于n和b的正整数，也被称为二项式系数，记为 $$\binom{n}{b}$$ 或者 $$\binom{n}{c}$$  

#### Threorem statement

>根据此定理，可以将x + y的任意次幂展开成和的形式  
$$(x + y) ^ n = \binom{n}{0}x^ny^0 + \binom{n}{1}x^n-1y^1 + \binom{n}{2}x^n-2y^2 + \cdot\cdot\cdot + \binom{n}{n-1}x^1y^n-1 + \binom{n}{n}x^0y^n$$  
wikipedia的定义足够正式，也非常完备，但是对于初学者而言，这样的定义是需要进行阐释的。


#### Solution


$$C_3^1 = \frac{3!}{1!2!}$$


#### Code
```cpp
```

#### Time Complexity


#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash'>
