---
layout: post
title: "Leetcode 25. Reverse Nodes in k Group"
date: 2017-09-14 19:00:00 +0800 
categories: 算法
tags: 
    - ds-linkedlist
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Remove Element

#### Description

> Given an array and a value, remove all instances of that value in place and return the new length.  
> Do not allocate extra space for another array, you must do this in place with constant memory.  
> The order of elements can be changed. It doesn't matter what you leave beyond the new length.  
> 
> Example:  
> Given input array nums = [3,2,2,3], val = 3  
> Your function should return length = 2, with the first two elements of nums being 2.

#### Solution

&emsp;&emsp;链表内部的翻转，要求内存空间为常数，所以不能使用数组或者vector，链表操作的话，特别是这种会改变链表结构的情况，都会使用dummy node。本题的思路是先找到要翻转数列中的最后一个节点，然后通过循环由后向前修改每个节点的next域，在整个过程中需要妥善保存first 和last节点的地址，first是需要翻转链表的首节点，last是需要翻转链表最后一个节点的下一个节点。在整个翻转过程中想清楚指针需要走多少步可以到目标指针。  
![leetcode25](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode25/leetcode25.png)

#### Code

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        
    }
};
```


#### Time Complexity

