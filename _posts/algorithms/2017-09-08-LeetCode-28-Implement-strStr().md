---
layout: post
title: "Leetcode 28. Implement strStr()"
date: 2017-09-14 19:00:00 +0800 
categories: 算法
tags: 
    - ds-string
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Implement strStr()

#### Description

> Implement strStr().  
> Retures the index of the first occurrence of needle in haystack, or -1 if needles is not part of haystack.  

#### Solution

&emsp;&emsp;题意是找needle这个string在haystack里面第一次出现的位置，可以for haystack里面的每一个位置，检查以这个位置开始的串是否与needle相同，但这个复杂度为O(n^2)。这里介绍下KMP算法，KMP算法可以将时间复杂度降低到O(m + n)的时间复杂度。  
&emsp;&emsp;KMP算法的实现建立在一个longest prefix suffix数组上，所以构建这个longest prefix suffix数组是KMP算法的第一步，那么什么是longeset prefix suffix数组？现在我们以LPS数组来代表longest prefix suffix数组，i代表LPS的下标，needle是我们的输入字符串，那么LPS[i]代表的是needle.substr(0, i + 1)(也就是说needle[0]~needle[i]所构成的字符串)中，既是longest proper prefix又是longest proper suffix的子字符串的长度，不明白什么意思？没关系，现在用实例来具体解释。  
&emsp;&emsp;有一个string : "abab"，那么它的proper prefixes就包括，"a"，"ab"，"aba"，同样的，它的proper suffixes就包括"b"，"ab"，"bab"，请注意，"abab"本身既不是proper prefix 也不是proper suffix，通过使用这个LPS数组保存到下标为i的字符为止的longest prefix suffix，对于"abab"而言，数组如下，所以LPS数组的内容是[0, 0, 1, 2]
$$\begin{array}{|c|c|}
\hline
a & b & a & b \\
\hline
0 & 0 & 1 & 2 \\
\hline
\end{array}$$，
对于字符串"aaaa"而言，我们应该得到LPS数组
$$\begin{array}{|c|c|}
\hline
a & a & a & a \\
\hline
0 & 1 & 2 & 3 \\
\hline
\end{array}$$，这里强调的就是longest prefix suffix不包括数组本身，综上，到每个needle每个字符的longest prefix suffix的长度组合起来，就构成了longest prefix suffix数组。  
&emsp;&emsp;现在就解释下，如何通过算法找到longest prefix suffix数组，构建好LPS。为了说明清楚这个算法的原理，我们先做一个假设，假设LPS[0]到LPS[i - 1]的值已经通过之前的计算得到，现在要求LPS[i]，定义j是needle[0] ~ needle[i - 1]的子串中longest prefix suffix的长度， 那么根据LPS的定义，下图中needle[0] ~ needle[j - 1]的字符串与needle[i - j] ~needle[i - 1]的字符串的值是相同的，请务必思考并理解这一点，这是在整个算法中，我们都会反复用到这个事实。
![leetcode26_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_01.png)  
&emsp;&emsp;接下来，如果needle[j] == needle[i]，那么我们可以知道这相当于在needle[0] ~ needle[j - 1] == needle[i - j] ~ needle[i - 1]的情况下，又知道needle[j] == needle[i]，那么很明显我们可以推导出，needle[0] ~ needle[j] == needle[i - j] ~ needle[i]，这个时候longest prefix suffix的长度就是j + 1，也就是说到needle[i]，longest prefix suffix的长度就是j + 1， 所以有LPS[i] = j + 1。  
![leetcode26_02](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_02.png)  
在得到了needle[i]之后，我们对i和j都自增一，再进行计算。  
![leetcode26_03](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_03.png)  
&emsp;&emsp;之前我们假设needle[j] == needle[i]，那么如果两者不想同呢？这个时候，根据定义，longest prefix suffix的长度就肯定不是j了，
![leetcode26_04](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_04.png)  
&emsp;&emsp;
#### Code

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int ret = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != val) {
                nums[ret++] = nums[i];
            }
        }
        return ret;
    }
};
```


#### Time Complexity

O(n);