---
layout: post
title: "leetcode 34. Search in Rotated Sorted Array"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - binarysearch
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Search in Rotated Sorted Array

#### Description

>Suppose a sorted array is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

>You are given a target value to search. If found in the array return its index, otherwise return -1.

>You may assume no duplicate exists in the array.

#### Solution

&emsp;&emsp;比较复杂的二分做法，需要判断出mid所在的部分是pivot的左边还是右边，对这两边的情况分开讨论就可以，这道题已经看到很多次了，不是很想讲解，如果需要的话，后期再做。

#### Code

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        if (nums.size() == 0) {
            return -1;
        }
        int start = 0;
        int end = nums.size() - 1;
        int mid;

        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[start] < nums[mid]) {
                if (nums[start] <= target && target <= nums[mid]) {
                    end = mid;
                } else {
                    start = mid;
                }
            } else {
                if (nums[mid] <= target && target <= nums[end]) {
                    start = mid;
                } else {
                    end = mid;
                }
            }
        }

        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    }
};
```


#### Time Complexity

O(n);