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

&emsp;&emsp;动态规划就是通过递推关系找到将当前问题简化为规模更小问题的途径，然后再通过初始化状态，逐渐衍生出问题答案的过程。本题最重要的思路就是构建一个matrix二维数组，数组x轴上的[s, 0, 1, 2, 3]代表与数组s[0, 1, 2, 3]的对应关系，数组y轴上的[p, 0, 1, 2, 3, 4]代表与数组p[0, 1, 2, 3, 4]的对应关系，在matrix数组中，多了两个元素，s, p 这两个元素分别代表s和p为空字符串的情况。整个解答过程就是将左下的二维数组填充成下右下的二维数组。  
![leetcode10_05](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_05.png)
![leetcode10_03](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_03.png)  
&emsp;&emsp;为了方便说明，以s = "abcd", p = "a\*.cd"为例，定义出二维矩阵如下左，初始化的第一步就是考虑s == "" 和 p == ""的情况，也就是matrix[0][0]，此时应该认为两者是匹配的，所以matrix[0][0] = true，矩阵转换成为下右的状态。 
![leetcode10_06](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_06.png)![leetcode10_07](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_07.png)  
&emsp;&emsp;接着分别考虑s != "" && p == ""的情况和s == "" && p != ""的两种情况。当s != "" && p == ""时，这就相当于给了一个字符串，却没有给匹配规则，这个时候还要问是否和匹配规则一致，这种情况下我们是无法给出答案的，所以默认全为false，于是得到下左的状态。当s == "" && p != ""时，这种情况，就只有在类似于p == "a*"的情况下两者才会匹配，其他情况均为不匹配，由此得到下右的状态，到此初始化结束。  
![leetcode10_08](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_08.png)![leetcode10_09](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_09.png)  
&emsp;&emsp;matrix的剩余部分就应该由递推公式来推导了，递推公式的规则我采用头脑风暴的形式进行说明，因为单靠语言已经很难表达出其中的逻辑关系，各位看官如果觉得图片不清晰，可以右键选择view image这样可以在单独的浏览器窗口中查看下图。  
![leetcode10_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode10/leetcode10_10.png)



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
