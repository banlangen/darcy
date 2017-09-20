---
layout: post
title: "leetcode 38. Count and Say"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Count and Say

#### Description

>>[原题请参考链接](https://leetcode.com/problems/sudoku-solver/description/)

#### Solution

&emsp;&emsp; 定义两个变量，count和prev，prev表示前一个字符是什么，count表示前一个出现字符的个数，当当前字符与前一个字符不相等的时候，就将前一个字符以及他的个数放到新的string中，同时还要注意，在字符串结束的时候，由于没有下一个字符了，所以这个时候不要忘记，还要将count和prev添加到最后的结果中去。

$$\begin{array}{c|c}
\hline
string & 1 & 2 & 1 & 1 \\
\hline 
count & 1 & 1 & 1 & 2 \\
\hline 
prev & 1 & 2 & 1 & 1 \\
\hline
\end{array}$$

#### Code

```cpp
class Solution {
public:
    string countAndSay(int n) {
        if (n <= 0) {
            return "";
        }
        string str = "1";
        for (int i = 1; i < n; i++) {
            int count = 0;
            char prev = '.';
            string sb;
            for (int idx = 0; idx < str.length(); idx++) {
                if (str[idx] == prev || prev == '.') {//将当前字符与其前面的一个字符相比，如果相等，count再加1，
                    count++;
                } else { //如果不等，就开始将计数与字符合并到一起并汇总到最后的字符串中。
                    stringstream ss;
                    ss << count;
                    sb += ss.str() + prev;
                    count = 1;
                }
                prev = str[idx];
            }
            stringstream ss;
            ss << count;
            sb += ss.str() + prev;
        }
        return str;
    }
};
```


#### Time Complexity

时间复杂度应该为O(n);