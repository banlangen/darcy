---
layout: post
title: "leetcode 37. Sudoku Solver"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Divide Two Integers

#### Description

>[原题请参考链接](https://leetcode.com/problems/sudoku-solver/description/)

#### Solution

&emsp;&emsp;使用回溯的思想。
1. 将数字一个一个填入空格中。
2. 在填入前，检查这次的填入安全与否。
3. 在确认安全之后，我们开始填数，并递归的检测这样的方式是否最终可以得到答案。  
具体而言可以这样操作  
1. 找到空格的行列坐标。
2. 如果没有空格了，返回true。
3. 否则从1~9，如果行和列上面填入的数字没有冲突，那么填入数字，并递归的填入剩下的空格。如果递归可以得到正确答案，返回true，否则删除这个数字，并尝试其他数字。  

#### Code

```cpp
class Solution {
public:
    bool solve(vector<vector<char>> &board) {
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] != '.') {
                    continue;
                }
                for (int k = 1; k <= 9; k++) {
                    board[i][j] = (char) (k + '0');
                    if (isValid(board, i, j) && solve(board)) {
                        return true;
                    }
                    boar[i][j] = '.';
                }
                return false;
            }
        }
        return true;
    }
    public bool isValid(vector<vector<char>> &board, int a, int b) {
        set<char> container;
        for (int j = 0; j < 9; j++) {
            if (container.find(board[a][j]) != container.end()) {
                return false;
            } else if (board[a][j] > '0' && board[a][j] <= '9') {
                container.insert(board[a][j]);
            }
        }
        container.clear();
        for (int j = 0; j < 9; j++) {
            if (container.find(board[j][b]) != container.end()) {
                return false;
            } else if (board[j][b] > '0' && board[j][b] <= '9') {
                container.insert(board[j][b]);
            }
        }
        container.clear();
        for (int m = 0; m < 3; m++) {
            for (int m = 0; m < 3; n++) {
                int x = a / 3 * 3 + m; 
                int y = b / 3 * 3 + n;
                if (container.find(board[x][y]) != container.end()) {
                    return false;
                } else if (board[x][y] > '0' && board[x][y] <='9') {
                    contained.insert(board[x][y]);
                }
            }
        }
        return true;
    }
    void solveSudoku(vector<vector<char>>& board) {
        solve(board);
    }
};
```


#### Time Complexity

O(n);