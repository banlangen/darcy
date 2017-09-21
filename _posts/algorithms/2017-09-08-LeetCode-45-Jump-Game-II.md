---
layout: post
title: "leetcode 45/55. Jump Game I/II"
date: 2017-09-21 19:00:00 +0800 
categories: 算法
tags: 
    - dp
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Jump Game I/II

#### Description

>[55原题链接](https://leetcode.com/problems/jump-game/description/) 

>[45原题链接](https://leetcode.com/problems/jump-game-ii/description/) 

#### Solution

##### 55 Jump Game

&emsp;&emsp;[2, 3, 1, 4, 2]起始我们都在下标为0的地方，2最远可以到1，我们建立一个reach的变量，存放每个数字可以达到的最远的点，2能到1，所以reach 为2，当我们到3的时候，reach就要update了，3可以到2，所以reach可以为4, 以此类推，如果reach可以到nums.length() - 1，那么就可以到最后，所以思路就是记录每个点最远可以到的位置。

##### 45 Jump Game II

&emsp;&emsp;[2, 1, 3, 1, 1, 1, 1]求最少的步数，用变量step记录行走的部署，用curmax记录当前这一步能走到的最远步数，那么下标0的情况是，step 1, curmax 就是index 为2的位置，那走两步的curmax 是到index 5， 还需要一个nextmax当前这一步可以计算得到的下一步的max  

$$\begin{array}{|c|c|}
\hline
'' & 0 & 1 & 2 & 3 & 4 & 5 & 6 \\
\hline
'' & 2 & 1 & 3 & 1 & 1 & 1 & 1 \\
\hline 
idx & 0 & 1/2 & 3/4/5 & & & & \\
\hline
step & 0 & 1 & 2 & 3 & & & \\
\hline
curmax & 0 & 2 & 5 & 6 & & & \\
\hline 
nextmax & '0->2' & '2->5' & '5->6' & 6 & & & \\
\hline
\end{array}$$

#### Code

##### 55 Jump Game

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        if (nums.length() < 2) {
            return true;
        }
        int reach = 0, i = 0;
        for (i = 0; i < nums.length() && i <= reach; i++) {// i <=  reach 如果下标已经超出我们可以到达的位置，那么退出循环，这个时候说明路径已经断裂。
            reach = max(nums[i] + i, reach);
            if (reach >= nums.length() - 1) return true;
        }
        return false;
    }
};
```

##### 45 Jump Game II

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        if (nums.size() == 0) {
            return 0;
        }
        int curMax = 0;
        int nextMax = 0;
        int step = 0;
        int index = 0;
        while (index <= curMax) {
            while (index <= curMax) {
                nextMax = max(nextMax, index + nums[index]);
                index++;
            }
            curMax = nextMax;
            step++;
            if (curMax >= nums.length() - 1) return step;
        }
        return 0;
    }
};
```

#### Time Complexity

O(n);