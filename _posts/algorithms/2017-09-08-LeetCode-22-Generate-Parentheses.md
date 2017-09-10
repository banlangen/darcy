---
layout: post
title: "Leetcode 22. Generate Parentheses"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - dfs
    - rcr2nonrcrs
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Generate Parentheses

#### Description

>Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.   

>For example, given n = 3, a solution set is: 

>For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.  

>[  
  "((()))",  
  "(()())",  
  "(())()",  
  "()(())",  
  "()()()"  
]

#### Solution

##### recursive

在整个获取字符串的过程中，L >= R 这个条件必须满足
有两个条件必须识别出来，我们以L和R分别代表"("的个数和")"的个数, n是程序的输入  
1. 当L < n时，可以继续放入"("，这点很重要，必须限制L，不能让L的增长超过n。    
2. 当R < L时，可以继续放入")"  
而当 L == R == n的时候整个过程结束

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