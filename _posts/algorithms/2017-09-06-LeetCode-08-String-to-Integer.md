---
layout: post
title: "Leetcode 08. String to Integer(atoi)"
date: 2017-09-05 19:00:00 +0800 
categories: 算法
tags: 
    - others
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## String to Integer(atoi)

#### Description

>Implement atoi to convert a string to an integer.

#### Solution

&emsp;&emsp;这个思路就是先判断正负号，然后根据后面的数值构建int型数值，特别要注意的是这个值很可能超过integer的可表示范围，为了防止溢出，我们需要用一个非常大的变量来存放可能的值，这个变量类型就是unsigned long long int可以表示的范围是[0, +18,446,744,073,709,551,615] 用语言已经很难描述这个值，大概是几千个亿个亿，绝对的天文数字，而这个值也是C++中int型中能表示的最大的整数范围，然后在输出的时候，再进行转换，整个思路用头脑风暴表示如下。  
![leetcode08](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode08/leetcode08.png)

#### Code

```cpp
class Solution {
public:
    int myAtoi(string str) {
        bool isNeg = false;
        unsigned long long int ret = 0;
        while (*str == ' ') {
            str++;
        }
        if (!isdigit(*str) || *str != '+' || *str = '-') {
            return 0;
        }
        if (*str == '+' || *str == '-') {
            if (!isdigit(*(str + 1))) {
                return 0;
            }
            if (*str == '-') {
                isNeg = true;
                str++;
            }
        }
        while (isdigit(*str)) {
            ret = ret * 10 + (*str - '0');
            if (ret > (unsigned long long int)INT_MAX) {
                return isNeg ? INT_MIN : INT_MAX;
            }
            str++;
        }
        return isNeg ? -(int)res : (int)res;
    }
};
```

#### Time Complexity

这道题的时间复杂度是O(n)，n是输入string的位数;
