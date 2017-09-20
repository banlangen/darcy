---
layout: post
title: "leetcode 40. Combination Sum II"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - dfs
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Combination Sum II

#### Description

>[原题链接](https://leetcode.com/problems/combination-sum-ii/description/)

#### Solution

&emsp;&emsp;典型的dfs试错回溯类的问题，这道题的要求是元素不重复取，所以需要考虑去重复的问题，而去重复的方法应该是使用sort排序后，然后跳过相同的字符。

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
            if (i > idx && candidates[i] == candidates[i - 1]) { //idx是本次递归取得第一个字符，而上一级递归取得必然是idx - 1的位置，去重的做法就是，我只允许连续的取值，但是不允许跳过，所以有了这么一句话。
                continue;
            }
            resItem.push_back(candidates[i]);
            helper(candidates, resItem, result, i + 1, target - candidates[i]);
            resItem.pop_back();
        }
    }
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> resItem;
        if (candidates.size() == 0) {
            return result;
        }
        sort(candidates.begin(), candidates.end());
        helper(candidates, resItem, result, 0, target);
        return result;
    }
};
```


#### Time Complexity

O(n);