---
layout: post
title: "Leetcode 10. Regular Expression Matching"
date: 2017-09-06 19:00:00 +0800 
categories: 算法
tags: 
    - dp
    - dfs
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Regular Expression Matching

#### Description

>implement regular expression matching with support for '.' and '\*'.
'.' Matches any single character.
'\*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).
The function prototype should be:  
bool isMatch(const char \*s, const char \*p)  
Some examples:  
isMatch("aa","a") → false  
isMatch("aa","aa") → true  
isMatch("aaa","aa") → false  
isMatch("aa", "a\*") → true  
isMatch("aa", ".\*") → true  
isMatch("ab", ".\*") → true  
isMatch("aab", "c\*a\*b") → true

---

#### Solution

#####  Dynamic Programming

&emsp;&emsp;动态规划就是通过递推关系找到将当前问题简化为规模更小问题的途径，然后再通过初始化状态，逐渐衍生出问题答案的过程。本题最重要的思路就是构建一个matrix二维数组，数组x轴上的[s, 0, 1, 2, 3]代表与数组s[0, 1, 2, 3]的对应关系，数组y轴上的[p, 0, 1, 2, 3, 4]代表与数组p[0, 1, 2, 3, 4]的对应关系，在matrix数组中，多了两个元素，s, p 这两个元素分别代表s和p为空字符串的情况。整个解答过程就是将左下的二维数组填充成下右下的二维数组。  
![leetcode10_05](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_05.png)
![leetcode10_03](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_03.png)  
&emsp;&emsp;为了方便说明，以s = "abcd", p = "a\*.cd"为例，定义出二维矩阵如下左，初始化的第一步就是考虑s == "" 和 p == ""的情况，也就是matrix[0][0]，此时应该认为两者是匹配的，所以matrix[0][0] = true，矩阵转换成为下右的状态。 
![leetcode10_06](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_06.png)![leetcode10_07](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_07.png)  
&emsp;&emsp;接着分别考虑s != "" && p == ""的情况和s == "" && p != ""的两种情况。当s != "" && p == ""时，这就相当于给了一个字符串，却没有给匹配规则，这个时候还要问是否和匹配规则一致，这种情况下我们是无法给出答案的，所以默认全为false，于是得到下左的状态。当s == "" && p != ""时，这种情况，就只有在类似于p == "a*"的情况下两者才会匹配，其他情况均为不匹配，由此得到下右的状态，到此初始化结束。  
![leetcode10_08](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_08.png)![leetcode10_09](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_09.png)  
&emsp;&emsp;matrix的剩余部分就应该由递推公式来填充了，需要注意的是数组的填充方向应该如下图所示，先自左向右，然后再自上而下，所以对于推导公式而言，应该是先执行列循环，再执行行循环。  
![leetcode10_12](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_12.png)  
&emsp;&emsp;递推公式的规则我采用头脑风暴的形式进行说明，因为单靠语言已经很难表达出其中的逻辑关系，各位看官如果觉得图片不清晰，可以右键选择view image这样可以在单独的浏览器窗口中查看下图。  
![leetcode10_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_10.png)  
&emsp;&emsp;最终我们得到结果如下的结果，而我们的答案就在matrix[5][4]这个位置上，matrix[5][4] == true，所以我们可以知道字符串abcd和规则a\*.cd匹配。  
![leetcode10_11](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_11.png)  

##### dfs
&emsp;&emsp;如果说动态规划有一种回顾过去的意味，那么深度优先遍历则带有一种探索与回溯的意味，探索意味着关注的是当前与未来，如果在探索过程中出现失误，随即进行回退，根据这个思路，用头脑风暴表现如下  
![leetcode10_13](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_13.png)

#### Code

#####  Dynamic Programming

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        vector<vector<bool>> matrix(p.length() + 1, vecotr<bool>(s.length() + 1, false));
        matrix[0][0] = true;
        //初始化matrix[i][0];
        for (int i = 0; i < p.length(); i++) {
            if (p[i] == '*') {
                matrix[i + 1][0] = matrix[i - 1][0];
            }
        }
        for (int i = 1; i < p.lenghth() + 1; i++) {
            for (int j = 1; j < s.length() + 1; j++) {
                if (p[i - 1] == '.') {
                    matrix[i][j] = matrix[i - 1][j - 1];
                } else if (p[i - 1] == '*') {
                    if (p[i - 2] != s[j - 1] && p[i - 2] != '.') {
                        matrix[i][j] = matrix[i - 2][j];
                    } else {
                        matrix[i][j] = matrix[i - 2][j] || matrix[i - 1][j] || matrix[i][j - 1];
                    }
                } else {
                    matrix[i][j] = matrix[i - 2][j] || matrix[i - 1][j] || matrix[i][j - 1];
                }
            }
        }
        return matrix[p.lenght()][s.length()];
    }
};
```

##### dfs

```cpp
class Solution {
public:
    /*
    题意： 正则表达式匹配，'.'可以匹配任意字符，'*'可以匹配任意个(可以为0)'*'之前的字符
    不考虑'*'的话，题目变成简单的匹配。考虑'*'，可能产生的情况有匹配0、1、2…个字符
    因此可以使用递归或dp或其他方法解决
    */
    bool isMatch(string s, string p) {
        if (s.length() == 0){
            // s串匹配完合法的情况只有p为空，或是 "X*X*"的形式
            if (p.length() & 1) return false;
            else {
                for (int i = 1; i < p.length(); i += 2) {
                    if (p[i] != '*') return false;
                }
            }
            return true;
        }
        if (p.length() == 0) return false;
        if (p.length() > 1 && p[1] == '*') {
            if (p[0] == '.' || s[0] == p[0]) {
                return isMatch(s.substr(1), p) || isMatch(s, p.substr(2));
            } else return isMatch(s, p.substr(2));
        } else {
            if (p[0] == '.' || s[0] == p[0]) {
                return isMatch(s.substr(1), p.substr(1));
            } else return false;
        }
    }
};
```

#### Time Complexity

这道题的时间复杂度是O(n)。
