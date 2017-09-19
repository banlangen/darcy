---
layout: post
title: "leetcode 36. Valid Sudoku"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - others
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Valid Sudoku

#### Description

> Determine if a Sudoku is valid.

[原题请看这里](https://leetcode.com/problems/valid-sudoku/description/)

#### Solution

&emsp;&emsp;数独游戏，想看每一行是否满足要求，再看每一列是否满足要求，最后看每一个3X3矩阵是否满足要求。

#### Code

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        if (board.size() == 0) {
            return false;
        }
        for (int row = 0; row < 9; row++) {
            vector<bool> taken(9, false);
            for (int idx = 0; idx < 9; idx++) {
                char c = board[row][idx];
                if (c != '.') {
                    int num = c - '1';
                    if (taken[num] == true) {
                        return false;
                    } else {
                        taken[num] = true;
                    }
                }
            }
        }

        for (int col = 0; col < 9; col++) {
            vector<bool> taken(9, false);
            for (int idx = 0; idx < 9; idx++) {
                char c = board[idx][col];
                if (c != '.') {
                    int num = c - '1';
                    if (taken[num] == true) {
                        return false;
                    } else {
                        taken[num] = true;
                    }
                }
            }
        }
        //box是一个3X3的矩阵，而九宫格里面一共有9个box。box / 3表示是第几行的box， 而box % 3 表示是第几列的box。
        for (int box = 0; box < 9; box++) {
            vector<bool> taken(9, false);
            for (int row = 0; row <3; row++) {
                for (int col = 0; col < 3; col++) {
                    char c = board[row + 3 * (box / 3)][col + 3 * (box % 3)];
                    if (c != '.') {
                        int num = c - '1';
                        if (taken[num] == true) {
                            return false;
                        } else {
                            taken[num] = true;
                        }
                    }
                }
            }
        }
    }
};
```


#### Time Complexity

O(n);