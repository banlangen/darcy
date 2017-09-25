---
layout: post
title: "leetcode 52. N-Queens-II"
date: 2017-09-25 19:00:00 +0800 
categories: 算法
tags: 
    - dfs
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## N-Queens-II

#### Description

>Follow up for N-Queens problem.

>Now, instead outputting board configurations, return the total number of distinct solutions.

#### Solution

&emsp;&emsp;深度优先遍历

#### Code

```cpp
class Solution {
public:
    void dfs(vector<int> &col, vector<int> &diag_x, vector<int> &diag_y, int &count, int row, int size) {
        if (row == size) {
            count++;
            return;
        }
        
        for (int i = 0; i < size; i++) {
            if (col[i] && diag_x[row + i] && diag_y[row - i + size - 1]) {
                col[i] = diag_x[row + i] = diag_y[row - i + size - 1] = false;
                dfs(col, diag_x, diag_y, count, row + 1, size);
                col[i] = diag_x[row + i] = diag_y[row - i + size - 1] = true;
            }
        }
    }
    
    int totalNQueens(int n) {
       vector<int> col(n, true);
       vector<int> diag_x(2 * n - 1, true);
       vector<int> diag_y(2 * n - 1, true);
       int count = 0;
       dfs(col, diag_x, diag_y, count, 0, n);
       return count;
    }
};
```


#### Time Complexity

O(n);