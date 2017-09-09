---
layout: post
title: "Leetcode 22. Generate Parentheses"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - dfs
    - bfs
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

在整个获取字符串的过程中，L >= R 这个条件必须满足
有两个条件必须识别出来，我们以L和R分别代表"("的个数和")"的个数, n是程序的输入  
1. 当L < n时，可以继续放入"("，这点很重要，必须限制L，不能让L的增长超过n。    
2. 当R < L时，可以继续放入")"  
而当 L == R == n的时候整个过程结束
#### Code

还是回溯法，以n=3 为例子，

[code source](http://www.jiuzhang.com/solution/4sum '取自九章算法')  
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

#### Time Complexity

找到数列中所有和等于目标数的四元组，需去重多枚举一个数后，参照3Sum的做法，O(N^3)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">