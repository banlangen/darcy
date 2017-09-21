---
layout: post
title: "leetcode 44. Wildcard Matching"
date: 2017-09-21 19:00:00 +0800 
categories: 算法
tags: 
    - dp
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Wildcard Matching

#### Description

>[原题链接](https://leetcode.com/problems/wildcard-matching/description/)

#### Solution

&emsp;&emsp;建立如下的bool型数组，size是 (m + 1)(n + 1)所以是s字符串的长度+1，与p字符串长度+1，代表的意义，比如[i][j]:s中i长度的字符串与p中j长度的字符串是否匹配，比如s "abc", 与p "abdef"，如果有[2][2]代表的是s中的"ab"p中的"ab"是否match，match的话值就是true，
$$\begin{array}{|c|c|}
\hline
p\s & a & b & c \\
1 & & & \\
\hline
2 & & & \\
\hline 
3 & & & \\
\hline
end{array}$$

#### Code

```cpp
class Solution {
public:
    int divide(int dividend, int divisor) {
        
    }
};
```


#### Time Complexity

O(n);