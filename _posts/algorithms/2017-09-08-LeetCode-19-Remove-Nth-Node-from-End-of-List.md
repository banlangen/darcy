---
layout: post
title: "Leetcode 19. Remove Nth Node From End of List"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - s&f pointers
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

#### Solution

这道题的要求是“Try to do this in one pass”, 所以常规的解就不适用了，为了在1次遍历中找到并删除节点，就需要特别的思路，这里就是slow and fast pointers。  
![leetcode19_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode19/leetcode19_01.png)  
开始的时候，我们需要定义两个指针slow和fast, 同时让fast指针先向后移动n个位置, n就是本题的输入，然后就是同时移动slow和fast指针，当fast->next == NULL 的时候，slow->next == target。
其中有两个需要注意的点，第一是fast->next == NULL结束，而不是fast == NULL, 第二个就是当我们需要__改动链表结构__的时候都需要使用dummy node, 所以务必使用dummy node, 不要问我为什么，自己推导下就ok了。

#### Code

[code source](http://www.jiuzhang.com/solution/4sum '取自九章算法')  
```cpp
class Solution {
public:
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