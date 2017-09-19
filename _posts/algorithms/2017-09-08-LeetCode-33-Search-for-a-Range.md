---
layout: post
title: "leetcode 34. Search for a Range"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Search for a Range

#### Description

>Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.  
your algorithm's runtime complexity must be in the order of O(logn).  
if the target is not found in the arraym=, return [-1, -1].

>For example,  
Give [5,7,7,8,8,10] and target value 8,  
return [3,4].

#### Solution

&emsp;&emsp;典型的二分法的解答，需要分两个步骤，先用二分寻找最左边的下标，再用二分寻找最右边的下标。

#### Code

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        if (nums.size() == 0) {
            return {-1, -1};
        }
        int start , end, mid;
        vector<int> bound(2, -1);

        //search for the left bound.
        start = 0;
        end = nums.size() -1 ;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (nums[mid] >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[start] == target) {
            bound[0] = start;
        } else if (nums[end] == target) {
            bound[0] = end;
        } else {
            return bound;
        }

        //search for the right bound.
        start = 0;
        end = nums.size() - 1;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (nums[mid] <= target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (nums[end] == target) {
            bound[1] = end;
        } else if (nums[start] == target) {
            bound[1] = start;
        } else {
            return bound;
        }

        return bound;
    }
};
```


#### Time Complexity

O(logn);