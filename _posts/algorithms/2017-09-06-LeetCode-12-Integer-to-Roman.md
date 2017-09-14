---
layout: post
title: "Leetcode 12. Integer to Roman"
date: 2017-09-06 19:00:00 +0800 
categories: 算法
tags: 
    - div&mod
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Integer to Roman

#### Description

>Given an integer, convert it to a roman numeral.

>Input is guaranteed to be within the range from 1 to 3999

#### Back Ground

&emsp;&emsp;罗马数字的基本元素是。  
$$\begin{array}{|c|c|} 
\hline
I & V & X & L & C & D & M \\
\hline
1 & 5 & 10 & 50 & 100 & 500 & 1000 \\
\hline  
\end{array}$$

#### Solution

#####  Division & Modulus

&emsp;&emsp;罗马数字的个位数，十位数，百位数以及千位数的表示是各不相同的，也就是说每一个位数上都有一套自己的表示方法，而且每一个位数上的形式是可以列举出来的，如果能够将传入的十进制数的每一个位数抽取出来，自然就可以将两者对应起来。

&emsp;&emsp;列举罗马数字的个位数，十位数，百位数以及千位数的表示，可以用到数组，然后用数组下标来引用数组元素。 
```cpp
vector<string> M = {"", "M", "MM", "MMM"};
vector<string> C = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
vector<string> X = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
vector<string> I = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
```

&emsp;&emsp;解析输入的整数，将解析结果与M ，C，X数组下标对应。需要用到商和余数的关系，已知对应关系 M->1000, C->100, X->10, 所以假设输入数字为N, 那么 N / M 得到的是 N 由多少个M组成，而N % M 得到的就是余下的余料，该余料肯定小于M，相当于排除了M位。根据这个原则，对于千位而言，由于最大是3999，所以可以知道千位上的十进制树是 N / M，要求百位上的数，作法就是先对千位取余数，这样就去掉了千位上的干扰，然后再对百位整除，以此类推，可以用一条语句了描述
```cpp
M[n / 1000] + C[n % 1000 / 100] + X[n % 100 / 10] + I[n % 10]
```

#### Code

```cpp
class Solution {
public:
    string intToRoman(int n) {
        vector<string> M = {"", "M", "MM", "MMM"};
        vector<string> C = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        vector<string> X = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        vector<string> I = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"}

        string res = M[n / 1000] + C[n % 1000 / 100] + X[n % 100 / 10] + I[n % 10];
        return res;
    } 
};
```

#### Time Complexity

这道题的时间复杂度是O(1);
