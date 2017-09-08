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

>Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.  
The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not. 

#### Solution

这是一道检查stack概念的例题，可以采用一个符号栈，思路就是遇到'(', '[', '{' 就入栈，遇到')', ']', '}'就检查栈顶看是否匹配，如果不匹配，return false, 如果匹配，出栈，继续检查。

#### Code

```cpp
class Solution {
public:
    bool isValidParenthese(string s) {
        stack<int> st;
        for (int i = 0; i < s.length(); i++) {
            if (s[i] == '(' || s[i] == '[' || s[i] == '{') {
                st.push(s[i]);
            } else {
                if (s[i] == ')' && st.top() != '(') {
                    return false;
                }
                if (s[i] == ']' && st.top() != '[') {
                    return false;
                }
                if (s[i] == '}' && st.top() != '}') {
                    return false;
                }
                st.pop();
            }
        }
        if (!st.empty()) {
            return false;
        } else {
            return true;
        }
    }
};
```

#### Time Complexity

遍历所有的数组元素，所以是O(n)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">