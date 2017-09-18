---
layout: post
title: "Leetcode 32 Longest Valid Parenthese"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - others
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Longest Valid Parentheses

#### Description

>Given a string containing just the characters '(' and ')', find the length of the longest valid(well-formed) parentheses substring.  
For "(()", the longest valid parentheses substring is "()", which has length = 2.  
Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4. 

#### Solution

&emsp;&emsp;我们用"(()())())"我们用到一个数据结构stack，定义一个idx初始值为-1，只要遇到一个'('我们就将它的index推入到stack中，定义一个leftmost下标，代表当前string最左侧的边界，初始为-1，当遇到')'我们将stack的栈顶pop出来，并计算当前读入数据的下标和pop之后栈顶的下标之间的差值，更新到maxlen变量中
$$\begin{array}{|c|c|}
\hline
string & idx & leftmost & stack & pop & maxlen \\
\hline
( & 0 & -1 & 0 & & 0 \\
\hline 
( & 1 & -1 & 01 & & 0 \\
\hline 
) & 2 & -1 & 0 & 1 & 2 \\ 
\hline 
( & 3 & -1 & 03 & & 2 - 0 \\
\hline
) & 4 & -1 & 0 & 3 & 4 - 0 \\
\hline
\end{array}$$


#### Code

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        
    }
};
```


#### Time Complexity

O(n);