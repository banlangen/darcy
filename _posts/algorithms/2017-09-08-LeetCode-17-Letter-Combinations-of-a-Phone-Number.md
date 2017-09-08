---
layout: post
title: "Leetcode 17. Letter Combinations of a Phone Number"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - C++
    - Algo
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Letter Combinations of a Phone Number

#### Description

>Given a digit string, return all possible letter combinations that the number could represent.  
A mapping of digit to letters (just like on the telephone buttons) is given below.  

>![image](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode17/leetcode17_01.png)  

>Input:Digit string "23"  
Output : ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].  

>Note:  
Although the above answer is in lexicographical order, your answer could be in any order you want.

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