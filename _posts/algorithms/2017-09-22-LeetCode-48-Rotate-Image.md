---
layout: post
title: "leetcode 48. Rotate Image"
date: 2017-09-22 19:00:00 +0800 
categories: 算法
tags: 
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Rotate Image

#### Description

>[原题链接](https://leetcode.com/problems/rotate-image/description/)

#### Solution

<div>
<video id='movie' width='90%' controls poster='http://ovwkcbdpf.bkt.clouddn.com/image/videopostert.png'>
    <source src='http://ovwkcbdpf.bkt.clouddn.com/image/leetcode48/2017-09-22-LeetCode-48-Rotate-Image.webm' type = 'video/webm'>
    Your browser does not support the video tag.
</video>
</div>
<script type='text/javascript'>document.getElementById('movie').style.height=document.getElementById('movie').scrollWidth*0.8+'px'</script>

#### Code

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        if (matrix.size() == 0) {
            return;
        }
        int top = 0;
        int left = 0;
        int right = matrix[0].size() - 1;
        int bottom = matrix.size() - 1;
        int n = matrix.size();
        while (n > 1) {
            for (int i = 0; i < n - i; i++) {
                int tmp = matrix[top][left + i];
                matrix[top][left + i] = matrix[bottom - i][left];
                matrix[bottom - i][left] = matrix[bottom][right - i];
                matrix[bottom][right - i] - matrix[top + i][right];
                matrix[top + i][right] = tmp;
            }
            top++;
            bottom--;
            left++;
            right--;
            n -= 2;
        }
    }
};
```


#### Time Complexity

O(n);