---
layout: post
title: "leetcode 47. Permutations II"
date: 2017-09-22 19:00:00 +0800 
categories: 算法
tags: 
    - dfs
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Permutations

#### Description

>[原题链接](https://leetcode.com/problems/permutations-ii/description/)

#### Solution

&emsp;&emsp;典型的dfs的例题，相对于46题，需要考虑排序后去重的问题。

#### Code

```cpp
class Solution {
public:
    void helper(vector<int> &nums, vector<vector<int>> &res, vector<int> &item, vector<bool> &used) {
        if (item.size() == nums.size()) {
            res.push_back(item);
            return;
        }
        
        for (int i = 0; i < nums.size(); i++) {
            if (used[i] == true || (i > 0 && nums[i - 1] == nums[i] && used[i - 1] == false)) {
                continue;
            }
            item.push_back(nums[i]);
            used[i] = true;
            helper(nums, res, item, used);
            used[i] = false;
            item.pop_back();
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> item;
        if (nums.size() == 0) {
            return res;
        }
        vector<bool> used(nums.size(), false);
        sort(nums.begin(), nums.end());
        helper(nums, res, item, used);
        return res;
    }
};
```


#### Time Complexity

O(n);