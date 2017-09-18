---
layout: post
title: "Leetcode 29. Divide Two Integers"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags : 
    - others
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Divide Two Integers

#### Description

> Divide two integers without using multiplication, division and mod operator.  
> If it is overflow, return MAX_INT. 

#### Solution

&emsp;&emsp;以32 / 3为例，先看除数，他比被除数小，所以把除数向左移动一位（第一次），3 << 1，这个动作相当于乘以2，3变成了6，6还是比32小，那么再向左移动一位（第二次），3 << 2，相当于$$3 \cdot 2^2$$，3变成12，然后再向左移动一位（第三次），3 << 3，相当于$$3 \cdot 2^3$$得到24，再向左移动一位（第四次），3 << 4相当于$$3 \cdot 2^4$$，这个时候发现48，比我们的被除数大了，所以将3向左移动了4次后，发现结果比32大了，那么只能向左移动3次，其含义是$$3 \cdot 2^3 = 24$$，32 - 24 = 8，接着看8 / 3的结果，同样，按照刚才的方法，要保证比8小，只能$$3 \cdot 2^1 = 6$$，最后8 - 6 = 2，2已经小于了除数3，运算结束，而32 / 3的结果，就是$$2^3 + 2^1 = 10$$。
&emsp;&emsp;注意需要考虑一些特殊情况，具体可以参考代码注释。

#### Code

```cpp
class Solution {
public:
    int divide(int dividend, int divisor) {
        if (divisor == 0) { //除数是0的话，返回最大值
            return INT_MAX;
        }
        if (dividend == INT_MIN) { //如果被除数是最小值的话，需要专门讨论。
            if (divisor == -1) { //如果除数为-1，注意负数的范围是[-2^(n-1) ~ 2^(n-1)-1]，所以负数的最小值如果直接去正，会溢出
                return INT_MAX;
            } else if (divisor == 1) {
                return IMT_MIN;
            }
        }
        long divd = (long)dividend;
        long divs = (long)divisor;
        int sign = 1; //注意符号
        if (divd < 0) {
            divd = -divd;
            sign = -sign;
        }
        if (dvis < 0) {
            divs = -divs;
            sign = -sign;
        }
        int res = 0;
        while (dvid >= divs) { //只要被除数还大于除数，继续。
            int shift = 0;
            while (divd >= divs << shift) { //对除数倍增直到除数大于被除数。
                shift++;
            }
            res += 1 << (shift - 1); //到底倍增了多少倍。
            divd -= divs << (shift - 1);
        }
        return sign * res;
    }
};
```


#### Time Complexity

O(n);