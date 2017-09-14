---
layout: post
title: "Leetcode 09. Palindrome Number"
date: 2017-09-05 19:00:00 +0800 
categories: 算法
tags: 
    - div&mod
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Palindrome Number

#### Description

>Determine whether an integer is a palindrome. Do this without extra space.

#### Solution

#####  Division & Modulus

&emsp;&emsp;假设给定number是n位十进制数字，那么通过$$\frac{number}{10^n}$$可以得到number的最高位数字，而通过$${number}%{10}$$可以得到number的个位数字，然后通过$$(number-\frac{number}{10^n}) \cdot 10^n$$可以去掉number的最高位数字。而$$\frac{number}{10}$$可以去掉number的最低位数字。这就是该题的最主要思路。

#### Code

```cpp
class Solution {
public:
    string isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        int div = 1; int num = x;
        while (num / div >= 10) {
            div *= 10;
        }
        while (num != 0) {
            int left = num / div;
            int right = num % 10;
            if (left != right) {
                return false;
            }
            num = (num - left * div) / 10;
            div /= 100;
        }  
    } 
};
```

#### Time Complexity

这道题的时间复杂度是O(n)，n是number的位数;
