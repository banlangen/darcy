---
layout: post
title: "Leetcode 22. Generate Parentheses"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - 2 pointers
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## 4Sum

#### Description

>Give an array S of n integers, are there elements a, b, c and d in S such that a + b + c + d = target ? Find all unique quadruplets in the array which gives the sum of target.  

>__Note__:The solution set must not contain duplicate quadruplets. 

>For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.  

>A solution set is :  
[  
  [-1, 0, 0, 1],  
  [-2, -1, 1, 2],  
  [-2, 0, 0, 2]  
]

#### Solution

没啥好说的，2 pointers做法，期间要经过两次循环转换成2Sum做法。  
详见其他几道2 pointers题目。

#### Code

[code source](http://www.jiuzhang.com/solution/4sum '取自九章算法')  
```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int len = nums.size();
        int left, right, sum;
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        vector<int> tmp;
        for (int i = 0; i < len - 3; i++) {
            if (i && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1; j < len - 2; j++) {
                if (j != i + 1 && nums[j] == nums[j - 1]) continue;
                sum = target - nums[i] - nums[j];
                left = j + 1;
                right = len - 1;
                while (left < right) {
                    if (nums[left] + nums[right] == sum) {
                        tmp.clear();
                        tmp.push_back(nums[i]);
                        tmp.push_back(nums[j]);
                        tmp.push_back(nums[left]);
                        tmp.push_back(nums[right]);
                        res.push_back(tmp);
                        left++;
                        right--;
                        while (left < right && nums[left] == nums[left - 1]) left++;
                        while (left < right && nums[right] == nums[right + 1]) right--;
                    } else 
                        if (nums[left] + nums[right] > sum) right--;
                        else left++;
                }
            }
        }
        return res;
    }
};
```

#### Time Complexity

找到数列中所有和等于目标数的四元组，需去重多枚举一个数后，参照3Sum的做法，O(N^3)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">