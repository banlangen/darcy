---
layout: post
title: "Leetcode 07. Reverse Integer"
date: 2017-09-04 19:00:00 +0800 
categories: 算法
tags: 
    - div&mod
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Reverse Integer

#### Description

>Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321 

#### Solution

&emsp;&emsp;通过一个循环，通过number % 10 每次取数字的最后一位，并通过number / 10去除最后一位，将得到的最后一位数字通过\* 10的方式放到新数字的最高位上面。使用C++的时候需要考虑溢出问题。

#### Code

```cpp
class Solution {
public:
    int reverse(int x) {
        long y = 0; 
        while (x != 0) {
            y = y * 10 + x % 10;
            x /= 10;
        }
        return y;     
    }
};
};
```

#### Time Complexity

这道题的时间复杂度是O(n)，n是输入输入数字的位数;
