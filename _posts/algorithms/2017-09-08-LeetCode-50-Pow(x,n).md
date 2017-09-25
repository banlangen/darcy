---
layout: post
title: "leetcode 50. Pow(x, n)"
date: 2017-09-25 19:00:00 +0800 
categories: 算法
tags: 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Pow(x, n)

#### Description

>Implement pow(x, n).

#### Solution

##### Iteration

<div>
<video id='movie' width='90%' controls poster='http://ovwkcbdpf.bkt.clouddn.com/image/videopostert.png'>
    <source src='http://ovwkcbdpf.bkt.clouddn.com/image/leetcode50/2017-09-22-LeetCode-50-Rotate-Image.webm' type = 'video/webm'>
    Your browser does not support the video tag.
</video>
</div>
<script type='text/javascript'>document.getElementById('movie').style.height=document.getElementById('movie').scrollWidth*0.8+'px'</script>

##### Recursion



#### Code

##### Iteration

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if (x == 1 || n == 0) {
            return 1;
        }
        double num = x;
        double res = 1;
        int pow = n;
        if (pow < 0) {
            num = 1 / x;
            if (pow == INT_MIN) {
                pow = INT_MAX - 1;
            } else {
                pow = -pow;
            }
        }
        while (pow != 0) {
            if (pow & 1) {
                res *= num;
                pow -= 1;
            } else {
                num *= num;
                pow /= 2;
            }
        }
        return res;
    }
};
```

##### Recursion

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if (x == 1 || n == 0) {
            return 1;
        }
        
        if (n < 0) {
            x = 1 / x;
            n = abs(n); //在C++中对INT_MIN取绝对值其实是一个未定义行为，但在运行这条代码的时候，没有发生异常。
        }
        return helper(x, n);
    }
    
    double helper(double x, int n) {
        if (n == 1) {
            return x;
        }
        if (n == 0) {
            return 1;
        }
        
        double t = helper(x, n / 2);
        if (n % 2 == 0) {
            return t * t;
        }else {
            return t * t * x;
        }
    }
};
```

#### Time Complexity

O(n);