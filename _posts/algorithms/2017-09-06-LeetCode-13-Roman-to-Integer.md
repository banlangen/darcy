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

罗马数字的基本元素是  
$$
\begin{array}{c|c} 
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
\end{array}
$$


##### no-recursive

如果用none recursive的话，主要的逻辑不变，使用stack，同时需要使用一个数据结构同时保存L, R, 以及当时构成的string.

#### Code

##### recursive

```cpp
class Solution {
public:
    void dfs(string s, vector<string> &res, int l, int r, int n) {
        if (r == n) {
            res.push_back(s);
        } else {
            if (l > r) {
                dfs(s + ')', res, l, r + 1, n);
            }
            if (l < n) {
                dfs(s + '(', res, l + 1, r, n);
            }
        }
    }

    vector<string> generateParenthesis(int n) {
        vector<string> res;
        string s;
        dfs(s, res, 0, 0, n);
        return res;
    }
};
```

##### non-recursive

```cpp
class Node {
public:
    string str;
    int l;
    int r;
    Node(string i_str, int i_l, int i_r) {
        l = i_l;
        r = i_r;
        str = i_str;
    }
}
class solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        stack<Node> st;
        st.push(Node("", 0, 0));
        while (!st.empty()) {
            Node cur = st.top();
            st.pop();
            if (cur.l == n && cur.r == n) {
                res.push_back(cur.str);
                continue;
            }
            if (cur.l > cur.r) {
                st.push(Node(cur.str + ")", cur.l, cur.r + 1));
            }
            if (cur.l < n) {
                st.push(Node(cur.str + "(", cur.l + 1, cur.r));
            }
        }
        return res;
    }
}
```

#### Time Complexity

这道题的时间复杂度的计算有点复杂，O(n * Cat(n)), Cat(n) 代表的是CATALAN数简单的说是指数级的时间复杂度，

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">