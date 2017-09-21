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

&emsp;&emsp;建立如下的bool型数组，size是 (m + 1)(n + 1)所以是s字符串的长度+1，与p字符串长度+1，代表的意义，比如[i][j]:s中i长度的字符串与p中j长度的字符串是否匹配，比如s "abc", 与p "abdef"，如果有[2][2]代表的是s中的"ab"p中的"ab"是否match，match的话值就是true。  
$$\begin{array}{|c|c|}
\hline
"p\s" & a & b & c \\
\hline
1 & & & \\
\hline
2 & & & \\
\hline 
3 & & & \\
\hline
\end{array}$$
&emsp;&emsp;关键的是初始状态，先初始化s是空字符串的时候，如果p也是空，那么肯定是true，所以[0][0]肯定是true，对于[1][0]而言，如果是*的话，那么其实可以看[0][0]的情况，所以if[i] == '\*' [i][0] == [i-1][0]，所以推而广之当'\*'被认为是0个字符的时候，可以有[i - 1][j] == [i][j]，
#### Code

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        vector<vector<bool>> match(p.length() + 1, vector<bool>(s.length() + 1，false));
        match[0][0] = true;
        for (int i = 1; i < p.length() + 1; i++) {
            if (p[i - 1] == '*') {
                match[i][0] = match[i - 1][0];
            }
        }

        for (int j = 1; j < s.length() + 1; j++) {
            match[0][j] = false;
        }

        for (int k = 1; k < p.length() + 1; k++) {
            for (int l = 1; l < s.length() + 1; l++) {
                if (s[l - 1] == p[k - 1] || p[k - 1] == '?') {
                    match[k][l] = match[k - 1][l - 1];
                } else if (p[k - 1] == '*') {
                    match[k][l] = match[k - 1][l] || match[k][l - 1];
                }
            }
        }
        return match[p.length()][s.length()];
    }
};
```


#### Time Complexity

O(n);