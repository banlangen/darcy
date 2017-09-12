---
layout: post
title: "Leetcode 13. Roman to Integer"
date: 2017-09-06 19:00:00 +0800 
categories: 算法
tags: 
    - dfs
    - rcr2nonrcrs
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Roman to Integer

#### Description

>Given a roman numeral, convert it to an integer.   

>Input is guaranteed to be within the range from 1 to 3999

#### Solution

##### recursive

&emsp;&emsp;罗马数字的基本元素是，如果我们注意到一个事实，当一个较小的数字出现在一个较大的数字的左边，计算方法就是减去这个数字。当一个较小的数字出现在一个较大数字的右边，计算方法就是加上这个数字，如果a是较小的数字，b是较大的数字，ab 代表b - a, 而ba代表b + a, 所以ba - ab = 2a, 而这也是我们这道题的解法。  
$$\begin{array}{|c|c|} 
\hline
I & 1 \\
\hline
V & 5 \\
\hline 
X & 10 \\
\hline
L & 50 \\
\hline
C & 100 \\
\hline
D & 500 \\
\hline
M & 1000 \\
\hline 
\end{array}$$  
&emsp;&emsp;我们自左向右逐个取数字，默认情况下，我们直接累加遇到的数字，但是当我们发现紧邻的两个数字，前一个小于后一个的话，我们就应该知道这个时候我们多加了两个“前一个数字”.


#### Code

[code source](http://www.jiuzhang.com/solution/roman-to-integer)

```cpp
class Solution {
public:
    int romanToInt(string s) {
        int ans = 0;
        ans = toInt(s[0]);

        for (int i = 1; i < s.length(); i++) {
            ans += toInt(s[i]);
            if (toInt(s[i-1]) < toInt(s[i])) {
                ans -= toInt(s[i-1]) * 2;
            }
        }
        return ans;
    }   

    int toInt(char s) {
        switch(s) {
            case 'I' :
                return 1;
            case 'V' : 
                return 5;
            case 'X' :
                return 10;
            case 'L' :
                return 50;
            case 'C' :
                return 100;
            case 'D' :
                return 500;
            case 'M' :
                return 1000;
        }
        return 0;
    }
};
```

#### Time Complexity

这道题的时间复杂度是O(n);
