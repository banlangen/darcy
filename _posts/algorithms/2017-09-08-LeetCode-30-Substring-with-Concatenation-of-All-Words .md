---
layout: post
title: "Leetcode 30. Substring with Concatenation of All Words "
date: 2017-09-18 19:00:00 +0800 
categories: 算法
tags: 
    - ds-array
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Substring with Concatenation of All Words 

#### Description

> You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

>For example, given:  
s: "barfoothefoobarman"  
words: ["foo", "bar"]

>You should return the indices: [0,9].
(order does not matter).  

#### Solution

&emsp;&emsp;要求所有的words中的字符串都必须用到，不能重复，由于已知words中每个字符串的长度是相等的，那么可以假设words中每个字符串的长度为n。可以考虑对于s中的每一个长度为words中所有字符串的长度加和的子串，逐个取出固定长度为n的子串，形成一个数组，只要这个数组的内容和words中的内容一致，那么问题得解

#### Code

```cpp
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words) {
        vector<int> res;
        if (s.length() == 0 || words.size() == 0) {
            return res;
        }
        sort(words.begin(), words.end());
        int word_size = words[0].length();
        int words_len = words.size();

        vecotr<string> subStrs;
        for (int i = 0; i + word_size * words_len - 1 < s.legnth(); i++) {
            for (int j = i , k = 0; k < words_len; j += word_size, k++) {
                subStrs.push_back(s.substr(j, word_size));''
            }
            sort(subStrs.begin(), subStrs.end());
            bool flag = true;
            for (int k = 0; k < word_size; k++) {
                if (subStrs[k] != words[k]) {
                    flag = false;
                }
            }
            if (flag) {
                res.push_back(i);
            }
        }
        return res;
    }
};
```

#### Time Complexity

&emsp;&emsp;大家都知道排序的时间复杂度为nlogn，所以这道题的时间复杂度为n^2logn，当然我也意思到排序的时间复杂度上是需要探讨的，我们要考虑到这里是对字符串的排序，而不是对字符的排序，所以排序的时候还要考虑到每个排序字符的长度，而字符的长度又与s的长度有关系，所以我似乎觉得时间复杂度上应该比n^2logn多一些，单是多少有点拿不准，还待后续研究。 