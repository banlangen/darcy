---
layout: post
title: "Leetcode 10. Regular Expression Matching"
date: 2017-09-06 19:00:00 +0800 
categories: 算法
tags: 
    - dp
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Regular Expression Matching

#### Description

>implement regular expression matching with support for '.' and '*'.
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).
The function prototype should be:  
bool isMatch(const char *s, const char *p)  
Some examples:  
isMatch("aa","a") → false  
isMatch("aa","aa") → true  
isMatch("aaa","aa") → false  
isMatch("aa", "a*") → true  
isMatch("aa", ".*") → true  
isMatch("ab", ".*") → true  
isMatch("aab", "c*a*b") → true


#### Solution

#####  Dynamic Programming

&emsp;&emsp;动态规划就是通过递推关系找到将当前问题简化为规模更小问题的途径，然后再通过初始化状态，逐渐衍生出问题答案的过程。要知道字符串S是否满足表达式P的规则，可以通过判断S.substr(0, S.length() - 1)这个子串是否和P的某一个子串匹配，这里说P的某一个子串，而不是P.substr(0, P.length() - 1)，原因是字符串和表达式的长度和匹配没有对应关系，可以是一个长字符串匹配短表达式如[abbbb]->[ab*], 也可以是一个短字符匹配长表达式如[a] -> [ab*c*]，

#### Code

```cpp
class Solution {
public:
    int maxArea(vector<int> &height) {
        int area; 
        int left = 0;
        int right = height.size() - 1;
        while (left < right) {
            area = max(area, min(height[left], height[right]) * (right - left));
            if (height[left] < height[right]) {
                left++;
            } else if (height[left] > height[right]) {
                right--;
            } else {
                left++;
                right--;
            }
        }
        return area;
    }
};
```

#### Time Complexity

这道题的时间复杂度是O(n)。
