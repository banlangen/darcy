---
layout: post
title: "Leetcode 14. Longest Common Prefix"
date: 2017-09-07 19:00:00 +0800 
categories: 算法
tag: C++
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Longest Common Prefix

#### Description

>Write a function to find the longest common prefix string amonst an array of strings. 

#### Solution

##### Brute force

这道题是要求求一系列字符串的共同前缀，最暴力的解法就是采用一个二重循环，用j和i分别表示需要解析数组的行和列，也就是j遍历所有的字符串，而i遍历字符串中的字符。我们以第一行的字符串作为标杆（任何一个字符串都可以作为标杆，因为我们要求的LCP肯定是小于任何一个给定的字符串的，为了方便起见，选择第一个字符串）遍历其中的每一个字符，再以这个字符作为标杆，逐次的检查其他的所有字符串的对应位置是否为当前选出的标杆字符，遇到两种情况，程序宣告结束:  
1) i位置对于该字符串而言已经越界。  
2) i位置的字符与标杆字符（strs[0][i]）不同。

```cpp
string prefix = "";
for (int i = 0; i < strs[0].length(); i++) { //遍历第一个字符串的每一个字符
    for (int j = 1; j < strs.size(); j++) {//依次检查剩下字符串中i位置的字符
        if (i >= strs[j].size() || strs[j][i] != strs[0][i]) {//两个条件之一满足，程序退出
            return prefix;
        }
    }
    prefix += strs[0][i];
}
```

##### Optimization

#### Code

