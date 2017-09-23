---
layout: post
title: "leetcode 49. Group Anagrams"
date: 2017-09-23 19:00:00 +0800 
categories: 算法
tags: 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Group Anagrams

#### Description

>[原题链接](https://leetcode.com/problems/group-anagrams/description/)

#### Solution

&emsp;&emsp;使用hash表保存，并且对string进行排序。

#### Code

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        map<string, list<string>> hashmap;
        for (string s : strs) {
            string tmp = s;
            sort(tmp.begin(), tmp.end());
            if (hashmap.find(tmp) == hashmap.end()) {
                list<string> l;
                l.push_back(s);
                hashmap.insert(make_pair(tmp, l));
            } else {
                hashmap[tmp].push_back(s);
            }
        }
        for (map<string, list<string>>::iterator itr = hashmap.begin(); itr != hashmap.end(); itr++) {
            vector<string> vs;
            for (list<string>::iterator litr = (itr->second).begin(); litr != (itr->second).end(); litr++) {
                vs.push_back(*litr);
            }
            res.push_back(vs);
        }
        return res;
    }
};
```


#### Time Complexity

O(n);