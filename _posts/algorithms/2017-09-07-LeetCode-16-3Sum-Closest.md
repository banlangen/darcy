---
layout: post
title: "Leetcode 16. 3Sum Closest"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags:
    - 2 pointers
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## 3Sum Closest

#### Description

>Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>
>For example, give array S = {-1 2 1 -4}, and target = 1.
>
>The sum that is closest to the target is 2. (-1 + 2 + 1 = 2)

#### Solution

该问题的解法其实和leetcode 15题一样，都是通过将问题转换为2Sum问题，然后使用两根指针求解，具体解法可以直接参考以下代码，特别的，由于是求最值，所以不用特别考虑去重的问题。

#### Code
```cpp
class Solution {
public :
    int threeSumClosest(vecotr<int> nums, int target) {
        sort(nums.begin(), nums.end());
        int result = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < nums.size(); i++) {
            int start = i + 1;
            int end = nums.size() - 1;
            while (start < end) {
                if (abs(result - target) > abs(nums[i] + nums[start] + nums[end] - target)) {
                    result = nums[i] + nums[start] + nums[end];
                }
                if (nums[i] + nums[start] + nums[end] > target) {
                    start++;
                } else {
                    end--;
                }
            }
        }
        return result;
    }
};
```

#### Time Complexity

该算法如leetcode 15分析，时间复杂度为O(n^2)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">