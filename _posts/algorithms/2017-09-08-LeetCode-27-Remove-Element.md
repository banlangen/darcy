---
layout: post
title: "Leetcode 27. Remove Element"
date: 2017-09-14 19:00:00 +0800 
categories: 算法
tags: 
    - ds-array
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Remove Element

#### Description

> Given an array and a value, remove all instances of that value in place and return the new length.  
> Do not allocate extra space for another array, you must do this in place with constant memory.  
> The order of elements can be changed. It doesn't matter what you leave beyond the new length.  
> 
> Example:  
> Given input array nums = [3,2,2,3], val = 3  
> Your function should return length = 2, with the first two elements of nums being 2.

#### Solution

&emsp;&emsp;从头到尾遍历数组，如果元素值不等于给定值，计数加一。

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