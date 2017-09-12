---
layout: post
title: "Leetcode 12. Integer to Roman"
date: 2017-09-06 19:00:00 +0800 
categories: 算法
tags: 
    - others
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

#####  

&emsp;&emsp;罗马数字的个位数，十位数，百位数以及千位数的表示是各不相同的，也就是说每一个位数上都有一套自己的表示方法，


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
