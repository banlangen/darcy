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

>Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0 ? Find all unique triplets in the array which gives the sum of zero  
Note : The solution set must not contain duplicate triplets.  
For example, give array S = [-1, 0, 1, 2, -1, -4],  
A solution set is :  
[  
   [-1, 0, 1],  
   [-1, -1, 2]  
]

#### Solution


#### Code
```cpp
class Solution {
public :
    string longestCommonPrefix(vector<string> &str) {
        string prefix = "";
        for (int i = 0; i < strs[0].length(); i++) { //遍历第一个字符串的每一个字符
            for (int j = 1; j < strs.size(); j++) {//依次检查剩下字符串中i位置的字符
                if (i >= strs[j].size() || strs[j][i] != strs[0][i]) {//两个条件之一满足，程序退出
                    return prefix;
                }
            }
            prefix += strs[0][i];
        }
        return prefix;
    }
};
```

#### Time Complexity

该算法需要要遍历完所有的字符串的所有公共字符，假设传入的字符串数组有m个，而字符串最小长度为n, 那么这 m * n 个字符都需要进行对比，所以时间复杂度为 O(m * n)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash'>
