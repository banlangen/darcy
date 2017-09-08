---
layout: post
title: "Leetcode 19. Remove Nth Node From End of List"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - ds-list
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Remove Nth Node From End of List

#### Description

>Given a linked list, remove the nth node from the end of list and return its head.  
For example,  
  Given linked list: 1->2->3->4->5, and n = 2.  
  After removing the second node from the end, the linked list becomes  
  1->2->3->5.

>__Note__:  
Given n will always be valid.  
Try to do this in one pass.   
[  
  [-1, 0, 0, 1],    
  [-2, -1, 1, 2],  
  [-2, 0, 0, 2]  
]

#### Solution



#### Code

[code source](http://www.jiuzhang.com/solution/4sum '取自九章算法')  
```cpp
class Solution {
public:
    /*
    题意：
    */
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