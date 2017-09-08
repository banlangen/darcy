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

>![leetcode17_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode17/leetcode17_01.png)  

>Input:Digit string "23"  
Output : ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].  

>Note:  
Although the above answer is in lexicographical order, your answer could be in any order you want.

#### Solution
 
该题是典型的采用dfs求解的问题，可以把这个问题理解成一个树，以输入数字为“23”为例它的根节点是“”，树的第二层是2所对应的三个字母{a, b, c}， 第三层是3所对应的三个字母{d, e, f}，这样的话这棵树其实就是一个组合的结果<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
$$C_n^m =\frac{n!}{m!(n-m)!}$$，根据题意，{a, b, c}中取一个为$$P_3^1 = \frac{3!}{1!2!}$$，{d, e, f}中取一个为$$P_3^1 = \frac{3!}{1!2!}$$，所以$$P_3^1 \cdot P_3^1 = 9$$ 一共有9种组合方法，也就是树的叶节点有9个，我们需要做的就是遍历到树的叶节点，在从叶节点到根节点的过程中我们定义变量path来存在遍历过程中经过的节点，并在到达叶节点的时候将path存放到最后的结果result中。

这里提到树，只是为了让我们更好的理解dfs解法，并不需要去构建一个树出来，我们需要定义一个下标idx，让idx一个数字一个数字的移动，当idx指向了输入数字的最后一个位置之后，就说明我们到达了想象中的树的叶节点。  
![leetcode17_02](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode17/leetcode17_02.png)  

提到了dfs自然就要提到dfs的一个重要特性“回溯”，其实“回溯”不能说的dfs特有的，而应该是所有递归函数所有的特性。当我们获取了字符串“bd”之后，为了获取以“b”开头的下一个字符串，必须回退到path = {“b”}的状态，这个时候如下图的浅蓝色箭头一样，有了一个状态的回溯过程，然后再次从数字2的下一个数字3出发，选取除掉“d”之外的其他字符进行组合。
![leetcode17_03](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode17/leetcode17_03.png)
#### Code
```cpp
//代码来自[source](http://www.jiuzhang.com/solution/letter-combinations-of-a-phone-number "九章算法")
class Solution {
public :
    const vector<string> keyboard = {" ", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

    vector<string> letterCombinations (const string &digits) {
        if (digits == "") {
            return {};
        }
        vector<string> result;
        dfs(digits, 0, "", result);
        return result;
    }

    void dfs (const string &digits, size_t idx, string path, vector<string> &result) {
        if (idx == digits.size()) { //如果到达了树的叶节点
            result.push_back(path);
            return;
        }
        for (auto c : keyboard[digits[idx] - '0']) {
            dfs (digits, idx + 1, path + c, result);
        }
    }
};
```

#### Time Complexity

该算法如leetcode 15分析，时间复杂度为O(n^2)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">