---
layout: post
title: "leetcode 42. Trapping Rain Water"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - 2pointers
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Trapping Rain Water

#### Description

>[原题链接](https://leetcode.com/problems/trapping-rain-water/description/)

#### Solution

##### First

&emsp;&emsp;第一种解法在于建立两个数组，leftmax和rightmax分别代表在该点的左边的最大值和右边的最大值，那么对于每个点，只需要知道min(leftmax, rightmax)，就可以知道当前这个点可以容纳多少水，然后遍历所有的点，累加出所有的结果。

##### Second

&emsp;&emsp;对于左右两个高度而言，矮的高度决定了中间每个点可以蓄水的高度，现在有连个点分别是l, r，l从左向右移动，r从右向左移动，绿色是l和r走过的点，所以绿色是已知点，灰色是未知点，对于左边我们取最大的值，右边取最大的值，两个最大的值中的小值，决定了其中间点蓄水的高度，
![leetcode42_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode42/leetcode42_01.png)
#### Code

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        vector<int> leftmax;
        vector<int> rightmax(height.size(), 0);
        int lmax = 0;
        for (int i = 0; i < height.size(); i++) {
            leftmax.push_back(lmax);
            lmax = max(lmax, height[i]);
        }
        int rmax = 0;
        for (int j = height.size() - 1; j >= 0; j--) {
            rightmax[j] = rmax;
            rmax = max(rmax, height[j]);
        }
        
        int area = 0;
        for (int k = 0; k < height.size(); k++) {
            int value = min(leftmax[k], rightmax[k]);
            if (value > height[k]) {
                area += value - height[k];
            }
        }
        return area;
    }
};
```


#### Time Complexity

O(n);