---
layout: post
title: "Leetcode 31. Next Permutation"
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - others
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Next Permutation

#### Description

>  Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

>If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

>The replacement must be in-place, do not allocate extra memory.

>Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.  
1,2,3 → 1,3,2  
3,2,1 → 1,2,3  
1,1,5 → 1,5,1

#### Solution

&emsp;&emsp;要找下一个大的数，我们用一个实例来说明，比如找12642的下一个大的数字，那就是14226，也就是替换的是前面的2，那么如何找到这个该被替换的2呢？我们应该从最后一个数字向前看，这个时候可以知道6 > 4 > 2， 直到我们看到 2 < 6 > 4 > 2，这就说明在2这个位置，可以找到一个比当前数2大的数字，那这个比2大的合适的值是多少呢？我们要继续从2开始想右找，也就是从后面的6, 4, 2里面找到一个比2大，但是又最接近2的数，这么找下来就是4了。所以我们可以确定4应该在现在2的这个位置上，也就是现在从左到有确定了1，4那么剩下的就是6,2,2，那我们对剩下的这一部分进行一次由小到大的排序，就可以得到14226。

#### Code

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        if (nums.size() == 0) {
            return;
        }
        int replace = nums.size() - 2;
        while (replace >= 0) {
            if (nums[replace] < nums[replace + 1]) {
                break;
            }
            replace--;
        }
        if (replace < 0) {
            sort(nums.begin(), nums.end());
            return;
        }
        int lgrIdx = replace + 1;
        while (lgrIdx < nums.size() && nums[lgrIdx] > nums[replace]) {
            lgrIdx++;
        }
        int tmp = nums[replace];
        nums[replace] = nums[lgrIdx - 1];
        nums[lgrIdx - 1] = tmp;
        sort(nums.begin() + replace + 1, nums.end());
    }
};
```

#### Time Complexity

和字符串的长度相关，所以为O(n)