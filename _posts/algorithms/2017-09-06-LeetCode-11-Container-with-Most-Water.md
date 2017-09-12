---
layout: post
title: "Leetcode 11. Container with Most Water"
date: 2017-09-06 19:00:00 +0800 
categories: 算法
tags: 
    - 2 pointers
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Container with Most Water

#### Description

>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

>Note: You may not slant the container and n is at least 2.

#### Solution

#####  2 pointers

&emsp;&emsp;典型的双指针问题，定义两个指针left和right，比较左右两个指针，移动值为小的那个指针，原因是容器的容积是由值小的指针决定的，如果移动值大的指针，由于left 和 right之间的距离在初始状态已经是最大的了，所以移动大端只会使容积减少，而移动小端的话，则有可能得到一个更大的纵向上的值。

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
