---
layout: post
title: "Leetcode 16. 3Sum Closest"
date: 2017-09-08 19:00:00 +0800 
categories: 算法
tag: C++
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## 3Sum Closest

#### Description

>Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>
>For example, give array S = {-1 2 1 -4}, and target = 1.
>
>The sum that is closest to the target is 2. (-1 + 2 + 1 = 2)

#### Solution

首先解释下"must not contain duplicate triplets"的意思，它的要求是得到的三个**_下标_**不能重复，而不是值不重复的元素，这就是为何示例中的答案有[-1, -1, 2]。

此题如果暴力求解，时间复杂度应该会达到O(n^3), 其中n为输入数组的元素个数，这完全没有办法接受。如果仔细观察会发现此题可以转换成n-2个2Sum的问题，也就是从第一个元素开始到第n-2个元素结束，对每个元素求解2Sum。由leetcode 01我们知道2Sum可以做到O(n)的时间复杂度，所以整个3Sum的时间复杂度为O(n^2)，你可能会问为什么到n-2个元素结束？好的，我们现在就来解释下这个问题。具体的我们用i代表要取的答案的第一个元素的下标，要注意到题目要求最后求解的三个元素不得重复，所以我们需要规定只能从左向右依次取这三个数字，这样才能避免[-1, 0, 1] 和 [-1, 1, 0]这样的重复。用一个循环让i从0逐个增加, 当i取到下标为n-3的元素时，右边就只剩下下标[n-2], [n-1]两个元素了，如果i继续向右走，就没法取满两个元素。不过我们在代码实现的时候可以不用太担心，i仍然可以取从0 到 n-1, 原因后面会讨论。

在确定了i之后，剩下的就可以用leetcode 01的解法去解答这道题，但是需要注意的是，leetcode 01只要求给出一个答案，而这里要求给出所有的可能，所以找到合适的匹配之后还需要继续寻找，不能return，具体细节这个地方就不再赘述了。

现在我们想讨论另外一种解法，leetcode 01的解法中我们用到了额外的数据空间，创建了一个priority_queue<int>， 用于存放已经访问过的元素以及其对应的下标，而实际上我们并不是一定要用到这个额外的数据空间。

假设现在我们有一个从左向右依次增大的排序数组（为什么讨论排序数组后面会解释）其中定义l和r分别代表下要取的第二个和第三个元素的下标，初始的状态下，l为i+1, r为nums.size()-1, 只要l小于r, 我们就可以进入下面的一个循环    
![Given Array](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode15/leetcode15_01.png)  
此时nums[l] + nums[r]的值为3，而实际我们希望两者的加和等于1（nums[i] == -1），现在的加和大于目标加和值, 为了寻找可能的答案，需要降低加和的大小，所以只能向左移动r, 也就是r--  
![Given Array](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode15/leetcode15_02.png)  
此时nums[l]与nums[r]的加和等于目标值1, 其中一个备选答案已经找到，这个时候要注意，我们需要继续寻找答案，但是也要同时排除掉所有的重复答案，此时此刻，可以看出下图的红色画圈部分的值都是重复答案，由于数组已经排序，所以去重复非常简单，只需要看l的下一个位置值和r的上一个位置值是否分别与l, r位置上的值一样，如果一样就直接跳过。  
![Given Array](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode15/leetcode15_03.png)  
如此循环，直到l >= r, 循环结束，上面我们有提到i其实可以去到nums.size()-1, 原因就在于，n-3是i的最后一个l小于r的下标，再往下l就大于等于r了，故不是很有必要限制i的值  
![Give Array](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode15/leetcode15_04.png)  
以上的做法的前提条件便是需要数组是已排序的，所以在操作之前必须对数组进行sort。

这里容易忘记的是其实对于下标为i的元素，也会有重复的值，所以这个重复的值也应该直接跳过，使用的方法可以见后面代码。

#### Code
```cpp
class Solution {
public :
    vector<vector<int>> treeSum(vector<int> &nums) {
        vector<vector<int>> res;
        if (nums.size() <= 2) {
            return res;
        }
        sort(nums.begin(), nums.end()); //千万别忘了sort!!
        for (size_t i = 0; i < nums.size() - 2; i++) {
            //i中重复的元素需要全部跳过
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int target = -nums[i];
            int l = i + 1;
            int r = nums.size() - 1;
            while (l < r) {
                //跳过l中重复的元素
                if (l > i + 1 && nums[l - 1] == nums[l]) {
                    l++;
                    continue;
                }
                //l中重复元素跳过之后，r自然也会跳过

                int sum = nums[l] + nums[r];
                if (sum < target) {
                    l++;
                } else if (sum > target) {
                    r--;
                } else {
                    vector<int> triplet = {nums[i], nums[l], nums[r]};
                    res.push_back(triplet);
                    l++; //此时需要主动移动l, 否则在相等情况下l, r都不动的话，代码会陷入死循环
                }
            }
        }
        return res;
    }
};
```

#### Time Complexity

该算法如前面分析，2Sum的算法还是需要要遍历完所有的数组元素，所以时间复杂度为O(n^2)。

#### Video

<embed src='http://player.youku.com/player.php/sid/XMjkwMzEwNTAwNA==/v.swf' allowFullScreen='true' quality='high' width='800' height='600' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash' wmode="opaque">