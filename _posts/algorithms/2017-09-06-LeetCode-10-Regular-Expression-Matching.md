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

---

#### Solution

#####  Dynamic Programming

![leetcode10_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_01.png)

mmp文件下载链接[download mmp](http://ovwkcbdpf.bkt.clouddn.com/mindjet/leetcode10.mmap 'click here to download')

&emsp;&emsp;动态规划就是通过递推关系找到将当前问题简化为规模更小问题的途径，然后再通过初始化状态，逐渐衍生出问题答案的过程。本题最重要的思路就是构建一个matrix二维数组，数组x轴上的[s, 0, 1, 2, 3]代表与数组s[0, 1, 2, 3]的对应关系，数组y轴上的[p, 0, 1, 2, 3, 4]代表与数组p[0, 1, 2, 3, 4]的对应关系，我们需要做的就是
![leetcode10_02](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_02.png)
![leetcode10_02](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_02.png)
&emsp;&emsp;，

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
