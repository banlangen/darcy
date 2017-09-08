---
layout: post
title: "Leetcode 17. Letter Combinations of a Phone Number"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tags: 
    - dfs
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Letter Combinations of a Phone Number

#### Description

>Given a digit string, return all possible letter combinations that the number could represent.  
A mapping of digit to letters (just like on the telephone buttons) is given below.  

>![image](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode17/leetcode17_01.png)  

>Input:Digit string "23"  
Output : ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].  

>Note:  
Although the above answer is in lexicographical order, your answer could be in any order you want.

#### Solution
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default">**Powered by Mathjax**</script>  
该题是典型的采用dfs求解的问题，可以把这个问题理解成一个树，以输入数字为23为例它的根节点是""，树的第二层是2所对应的三个字母{a, b, c}， 第三层是3所对应的三个字母{d, e, f}，这样的话这棵树其实就是一个排列的结果 

$$P_n^m =\frac{n!}{(n-m)!}$$，根据题意，$$P_3^1 \cdot P_3^1$$  
![leetcode17_02](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode17/leetcode17_02.png)  


#### Code
```cpp
class Solution {
public :
    int threeSumClosest(vecotr<int> nums, int target) {
        sort(nums.begin(), nums.end());
        int result = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < nums.size(); i++) {
            int start = i + 1;
            int end = nums.size() - 1;
            while (start < end) {
                if (abs(result - target) > abs(nums[i] + nums[start] + nums[end] - target)) {
                    result = nums[i] + nums[start] + nums[end];
                }
                if (nums[i] + nums[start] + nums[end] > target) {
                    start++;
                } else {
                    end--;
                }
            }
        }
        return result;
    }
};
```

#### Time Complexity

该算法如leetcode 15分析，时间复杂度为O(n^2)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">