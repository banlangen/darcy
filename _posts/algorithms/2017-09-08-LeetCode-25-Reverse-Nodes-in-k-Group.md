---
layout: post
title: "Leetcode 25. Reverse Nodes in k Group"
date: 2017-09-14 19:00:00 +0800 
categories: 算法
tags: 
    - 
    - 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Generate Parentheses

#### Description

> Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.  
> k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.  
> You may not alter the values in the nodes, only nodes itself may be changed.
Only constant memory is allowed.  
For example,  
Given this linked list: 1->2->3->4->5  
For k = 2, you should return: 2->1->4->3->5  
For k = 3, you should return: 3->2->1->4->5   

#### Solution

&emsp;&emsp;链表内部的翻转，要求内存空间为常数，所以不能使用数组或者vector，链表操作的话，特别是这种会改变链表结构的情况，都会使用dummy node，
![leetcode25](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode25/leetcode25.png)

#### Code

```cpp
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        head = dummy;
        for (;;) {
            int res_node = 0;
            ListNode *last = head->next;
            for (int i = 0; i < k; i++) {
                if (last == NULL) {
                    break; 
                }
                res_node++;
                last = last->next;
            }
            if (res_node < k) {
                break;
            }

            ListNode *first = head->next;

            for (int j = 0; j < k; j++) {
                int index = k - 1 - j;
                ListNode *aim = first;
                while (index--) {
                    aim = aim->next;
                }
                head->next = aim;
                head = aim;
            }
            head->next = last;
        }
        return dummy->next;
    }
};
```


#### Time Complexity

这道题的时间复杂度的计算有点复杂，O(n * Cat(n)), Cat(n) 代表的是catalan数，后面我会对catalan数进行解析。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">