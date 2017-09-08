---
layout: post
title: "Leetcode 21. Merge Two Sorted List"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - sort
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Merge Two Sorted List

#### Description

>Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists. 

#### Solution

两个排序链表的合并，是merge sort的基础，一个while循环外加if判断，注意dummy node的用法，各位看官请直接看代码。

#### Code

```cpp
class Solution {
public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        ListNode *dummy = new ListNode(0);
        ListNode *tmp = dummy;
        while (l1 != NULL && L2 != NULL) {
            if (l1->val < l2->val) {
                tmp->next = l1;
                l1 = l1->next;
            } else {
                tmp->next = l2;
                l2 = l2->next;
            }
            tmp = tmp->next;
        }
        if (l1 != NULL) {
            tmp->next = l1;
        } else {
            tmp->next = l2;
        }
        return dummy->next;
    }
};
```

#### Time Complexity

依次遍历两个链表的所有元素，所以是O(n)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">