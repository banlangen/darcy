---
layout: post
title: "leetcode 35. Search Insert Position"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - binarysearch
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Divide Two Integers

#### Description

>Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

>You may assume no duplicates in the array.

>Here are few examples.  
[1,3,5,6], 5 → 2  
[1,3,5,6], 2 → 1  
[1,3,5,6], 7 → 4  
[1,3,5,6], 0 → 0 

#### Solution

&emsp;&emsp;简单的二分法。

#### Code

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        if (nums.size() == 0) {
            return 0;
        }

        int start = 0, end = nums.size() - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        if (nums[start] >= target) {
            return start;
        }
        if (nums[end] >= target) {
            return end;
        }

    }
};
```


#### Time Complexity

O(n);