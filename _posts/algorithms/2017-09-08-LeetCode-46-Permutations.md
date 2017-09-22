---
layout: post
title: "leetcode 46. Permutations"
date: 2017-09-18 19:00:00 +0800 
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

>[原题链接](https://leetcode.com/problems/permutations/description/)

#### Solution

&emsp;&emsp;典型的dfs的例题，本题要注意使用used数组来记录已经使用过的点。

#### Code

```cpp
class Solution {
public:
    void helper(vector<int> &nums, vector<int> &item, vector<vector<int>> &res, vector<bool> &used, int idx) {
        if (item.size() == nums.size()) {
            res.push_back(item);
            return;
        }
        
        for (int i = 0; i < nums.size(); i++) {
            if (used[i] == true) {
                continue;
            }
            item.push_back(nums[i]);
            used[i] = true;
            helper(nums, item, res, used, i + 1);
            used[i] = false;
            item.pop_back();
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> item;
        if (nums.size() == 0){
            return res;
        }
        vector<bool> used(nums.size(), false);
        helper(nums, item, res, used, 0);
        return res;
    }
};
```


#### Time Complexity

O(n);