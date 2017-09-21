---
layout: post
title: "leetcode 43. Multiply Strings"
date: 2017-09-21 19:00:00 +0800 
categories: 算法
tags: 
    - others
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Multiply Strings

#### Description

>[原题链接](https://leetcode.com/problems/multiply-strings/description/)

#### Solution

&emsp;&emsp;以string "23" 乘以string "45"为例，得到的string的长度应该为4，可以先建立一个长度为n1 + n2的数组来存放结果，现在我取出3 乘以5，由于有进位，所以最后的字符串变成了0015，然后取出2再与5相乘，结果是10， 这个时候结果10的起始位也就是说最低位0，是从字符串的下标为2的节点开始，对应上面，也就是0015中的1所在的位置，所以这个结果用字符串表示出来就是0100，2*5 + 3*5的结果就是0015 + 0100 = 0115，第三步就是3与4相乘，结果的最低位也是从字符串的下标为2的节点开始，所以结果就是0120, 与刚才的结果0115相加，得到结果是0235，第四步是2*4，结果的最低位从字符串的第1位开始，0800，加上刚才的结果就是1035，这个结果就是最后的结果，要注意的是，结果的最高位可能不是一个有效数字，可能是0，所以在返回结果的时候，需要去掉前面的0。
&emsp;&emsp;上面的相乘过程可以看到，每次的结果可能都有两位，所以定义一个posLow和posHigh两个指针，定义i, j分别代表两个乘数的位置，如果稍作推敲就可以发现i, j 与posHigh和posLow的关系，也就是posLow = i + j + 1; posHigh = i + j;

#### Code

```cpp
class Solution {
public:
    string multiply(string num1, string num2) {
        if (nums1.size() ==0 || nums2.size() == 0) {
            return "0";
        }
        int len1 = nums1.size();
        int len2 = nums2.size();
        vector<int> res(num1.size() + nums2.size());
        for (int i = len1 - 1; i >= 0; i--) {
            for (int j = len2 - 1; j >= 0; j--) {
                int mul = (nums1[i] - '0') * (nums2[j] - '0');
                int posLow = i + j + 1;
                int posHigh = i + j;
                mul += res[posLow];
                res[posLow] = mul % 10;
                res[posHigh] += mul / 10
            }
        }
        string ret;
        for (int i : res) {
            if (ret.size() == 0 && i == '0') {
                continue;
            }
            stringstream ss;
            ss << i;
            ret += ss.str();
        }
        return ret.size() == 0 ? '0' : ret;
    }
};
```

#### Time Complexity

O(n);