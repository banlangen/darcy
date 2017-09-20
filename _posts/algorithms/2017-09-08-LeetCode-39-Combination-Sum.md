---
layout: post
title: "leetcode 39. Combination Sum"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Combination Sum

#### Description

>[原题链接](https://leetcode.com/problems/combination-sum/description/)

#### Solution

&emsp;&emsp;典型的dfs试错回溯类的问题，这种问题在Suduko问题里面有过解释，这里不准备再行说明。

#### Code

```cpp
class Solution {
public:
    void helper(vector<int> &candidates, vector<int> &resItem, vector<vector<int>> &result, int idx, int target) {
        if (target == 0) {
            result.push_back(resItem);
            return;
        }
        if (target < 0) {
            return;
        }
        
        for (int i = idx; i < candidates.size(); i++) {
            resItem.push_back(candidates[i]);
            helper(candidates, resItem, result, i, target - candidates[i]);
            resItem.pop_back();
        }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> resItem;
        if (candidates.size() == 0) {
            return result;
        }
        helper(candidates, resItem, result, 0, target);
        return result;
    }
};
```


#### Time Complexity

O(n);