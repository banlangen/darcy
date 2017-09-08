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
开始的时候，我们需要定义两个指针slow和fast, 然后让fast指针先向后移动n个位置, n就是本题的输入，之后同时移动slow和fast指针，当fast->next == NULL 的时候，slow->next == target。
其中有两个需要注意的点，第一是fast->next == NULL结束，而不是fast == NULL, 第二个就是当我们需要*改动链表结构*的时候都需要使用dummy node, 所以务必使用dummy node, 不要问我为什么，自己推导下就ok了。

#### Code
 
```cpp
class Solution {
public:
    ListNode *removeNthFromEnd (ListNode *head, int n) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        ListNode *slow = dummy;
        ListNode *fast = dummy;
        for (int i = 0; i < n; i++) {
            fast = fast->next;
        }
        while (fast->next != NULL) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return dummy->next;
    }
};
```

#### Time Complexity

由于只遍历了一次链表，所以是O(n)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">