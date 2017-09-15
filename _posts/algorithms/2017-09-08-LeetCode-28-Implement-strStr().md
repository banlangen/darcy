---
layout: post
title: "Leetcode 28. Implement strStr()"
date: 2017-09-14 19:00:00 +0800 
categories: 算法
tags: 
    - ds-string
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Implement strStr()

#### Description

> Implement strStr().  
> Retures the index of the first occurrence of needle in haystack, or -1 if needles is not part of haystack.  

#### Solution

&emsp;&emsp;题意是找needle这个string在haystack里面第一次出现的位置

#### Code

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int ret = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != val) {
                nums[ret++] = nums[i];
            }
        }
        return ret;
    }
};
```


#### Time Complexity

O(n);