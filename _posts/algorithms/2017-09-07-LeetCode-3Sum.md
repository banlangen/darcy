---
layout: post
title: "Leetcode 15. 3Sum"
date: 2017-09-07 19:00:00 +0800 
categories: 算法
tag: C++
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Longest Common Prefix

#### Description

>Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0 ? Find all unique triplets in the array which gives the sum of zero.
>
>Note : The solution set must not contain duplicate triplets.
>
>For example, give array S = [-1, 0, 1, 2, -1, -4],
>
>A solution set is :
[  
   [-1, 0, 1],  
   [-1, -1, 2]  
]

#### Solution

首先解释下"must not contain duplicate triplets"的意思，它的要求是得到的三个**_下标_**不能重复，而不是值不重复的元素，这就是为何示例中的答案有[-1, -1, 2]。

此题如果暴力求解，时间复杂度应该会达到O(n^3), 其中n为输入数组的元素个数，这完全没有办法接受。如果仔细观察会发现此题可以转换成n-2个2Sum的问题，也就是从第一个元素开始到第n-2个元素结束，对每个元素求解2Sum。由leetcode 01我们知道2Sum可以做到O(n)的时间复杂度，所以整个3Sum的时间复杂度为O(n^2)，你可能会问为什么到n-2个元素结束？好的，我们现在就来解释下这个问题。具体的我们用i代表要取的答案的第一个元素的下标，要注意到题目要求最后求解的三个元素不得重复，所以我们需要规定只能从左向右依次取这三个数字，这样才能避免[-1, 0, 1] 和 [-1, 1, 0]这样的重复。用一个循环让i从0逐个增加, 当i取到下标为n-3的元素时，右边就只剩下下标[n-2], [n-1]两个元素了，如果i继续向右走，就没法取满两个元素。

在确定了i之后，剩下的就可以用leetcode 01的解法去解答这道题，但是需要注意的是，leetcode 01只要求给出一个答案，而这里要求给出所有的可能，所以找到合适的匹配之后还需要继续寻找，不能return，具体细节这个地方就不再赘述了。

现在我们想讨论另外一种解法，leetcode 01的解法中我们用到了额外的数据空间，创建了一个priority_queue<int>， 用于存放已经访问过的元素以及其对应的下标，而实际上我们并不是一定要用到这个额外的数据空间。

假设现在我们有一个从左向右依次增大的排序数组（为什么讨论排序数组后面会解释）其中定义l和r分别代表下要取的第二个和第三个元素的下标，  
![Given Array](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode15/leetcode15_01.png)  
此时nums[l] + nums[r]的值为3，而实际我们希望两者的加和等于1（nums[i] == -1），现在的加和大与目标加和值, 为了寻找可能的答案，需要降低加和的大小，所以只能向左移动r, 也就是r--  
![Given Array](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode15/leetcode15_02.png)  


#### Code
```cpp
class Solution {
public :
    string longestCommonPrefix(vector<string> &str) {
        string prefix = "";
        for (int i = 0; i < strs[0].length(); i++) { //遍历第一个字符串的每一个字符
            for (int j = 1; j < strs.size(); j++) {//依次检查剩下字符串中i位置的字符
                if (i >= strs[j].size() || strs[j][i] != strs[0][i]) {//两个条件之一满足，程序退出
                    return prefix;
                }
            }
            prefix += strs[0][i];
        }
        return prefix;
    }
};
```

#### Time Complexity

该算法需要要遍历完所有的字符串的所有公共字符，假设传入的字符串数组有m个，而字符串最小长度为n, 那么这 m * n 个字符都需要进行对比，所以时间复杂度为 O(m * n)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash'>
