---
layout: post
title: "Leetcode 28. Implement strStr()"
date: 2017-09-14 19:00:00 +0800 
categories: 算法
tags: 
    - KMP
---
* content
{:toc}

这里收集[`LeetCode`](https://leetcode.com)上的算法题目，并根据能找到的解答，加上自己的理解和思考，重新整理。

<!-- more -->

## Implement strStr()

#### Description

> Implement strStr().  
> Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.  

#### Solution

&emsp;&emsp;题意是找needle这个string在haystack里面第一次出现的位置，可以for haystack里面的每一个位置，检查以这个位置开始的串是否与needle相同，但这个复杂度为O(n^2)。这里介绍下KMP算法，KMP算法可以将时间复杂度降低到O(m + n)的时间复杂度。  
&emsp;&emsp;在讲解算法之前，我们先说明一个数组下标与长度这个有时候容易让编程人员犯错误的问题，请问数组下标i和下标j之间(包括i和j，且j > i)到底有多少个元素？是j - i吗？如果你觉得是的话，请看下面的例子，请问infinity中第一个字符i和t之间有多少个字符？是6 - 0 = 6吗？如果你数一数你就会发现是7个，也就是j - i + 1。所以反过来，从下标0开始，长度为7的字符串的最后一个元素的下标就应该是6，也就是i + lenghth - 1。  
$$\begin{array}{|c|c|}
\hline
i & n & f & i & n & i & t & y \\
\hline
0 & 1 & 2 & 3 & 4 & 5 & 6 & 7 \\
\hline
\end{array}$$  
&emsp;&emsp;由此展开，在下图中，如果问从下标0开始，长度为j的字符串的最后一个元素的下标是多少，你应该是知道是j - 1而不是j，而下标为j的字符是长度为j的字符的最后一个字符的下一个字符，在后面的讲解中如果你产生了一些疑问，我相信这段文字应该可以帮助到你。
![leetcode26_01](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_01.png)  
&emsp;&emsp;KMP算法的实现建立在一个longest prefix suffix数组上，所以构建这个longest prefix suffix数组是KMP算法的第一步，那么什么是longeset prefix suffix数组？现在我们以LPS数组来代表longest prefix suffix数组，i代表LPS的下标，needle是我们的输入字符串，那么LPS[i]代表的是needle.substr(0, i + 1)(也就是说needle[0]~needle[i]所构成的字符串)中，既是longest proper prefix又是longest proper suffix的子字符串的**长度**，不明白什么意思？没关系，现在用实例来具体解释。  
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
&emsp;&emsp;在得到了needle[i]之后，我们对i和j都自增一，再进行计算。  
![leetcode26_03](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_03.png)  
&emsp;&emsp;之前我们假设needle[j] == needle[i]，那么如果两者不想同呢？这个时候，根据定义，longest prefix suffix的长度就肯定不是j了，为了求得LPS[i]的正确值，我们需要意识到，needle[0] ~ needle[j - 1] == needle[i - j] ~ needle[i - 1]这个前提条件仍然成立，但是needle[j] != needle[i]的情况下，这个前提条件已经没有意义，那下一步我们需要做的就是找到needle[0] ~ needle[i - 1]的下一个最大的longest prefix suffix的长度，下图中表示为S，当我们找到之后，我们就需要更新j的值，然后再比较needle[j]和needle[i]，如果此时needle[i] == needle[j]那么LPS[i] = j + 1， 或者说是字符串S的长度 + 1。  
![leetcode26_05](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_05.png)  
&emsp;&emsp;现在我们来看如何找到这个S，先把j退回到之前的位置。  
![leetcode26_04](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_04.png)  
&emsp;&emsp;我们先假设我们已经找到了S，那么根据前面我们的定义，这个S肯定是needle[0] ~ needle[i - 1]之间的第二大proper prefix suffix，而已知needle[0] ~ needle[j - 1] == needle[i - j] ~ needle[i - 1]，所以我们可以得到needle[0] ~ needle[i + len(S) - 1] == needle[j - len(S)] ~ needle[j - 1]，也就是如下图所表示的  
![leetcode26_06](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_06.png)  
&emsp;&emsp;也就是说其实这个S也就是needle[0] ~ needle[j - 1]的longest proper suffix， 而这个longest proper suffix的长度已经算出来了，就是LPS[j - 1]。
![leetcode26_07](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_07.png)  
&emsp;&emsp;所以这个时候我们可以直接将j移动到S字符串的最后一个字符的下一个字符，然后再次比较needle[j]与needle[i]，S字符串的最后一个字符的下一个字符的下标是多少？就是LPS[j - 1]（提醒：LPS中存放的是长度，然后再参考开篇提到的数组下标和长度的关系）如果两者相等，那么LPS[i] = j + 1，如果两者不相等，那么继续重复刚才的步骤，寻找第三大proper prefix suffix，这个循环可以一直这么执行下去，要么我们找到合适的起点，使得needle[j] == needle[i]，要么继续循环，直到j == 0的时候，这说明实在找不到一个S使得S + needle[j] = S + needle[i]，所以这个时候LPS[i] = 0。 
![leetcode26_08](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_08.png)  
&emsp;&emsp;根据上面的讨论，代码可以总结为
```cpp
vector<int> lps(needle.length(), 0);
int j = 0;
int i = 1;
lps[0] = 0;

while (i < needle.length()) {
    if (needle[j] == needle[i]) {
        lps[i] = j + 1;
        j++;
        i++;
    } else { // needle[j] != needle[i])
        if (j != 0) {
            j = lps[j - 1];
        } else { // j == 0
            lps[i] = 0;
            i++;
        }
    }
}
```
&emsp;&emsp;以下视频用一个实例演示了代码的执行过程，抱歉引用youku的视频会被嵌入广告。  
<embed id='movie' src='http://player.youku.com/player.php/sid/XMzAyNzYzNjEzMg==/v.swf' allowfullscreen='true' quality='high' width='90%' align='middle' allowscriptaccess='always' type='application/x-shockwave-flash'/>  
<script type='text/javascript'>document.getElementById('movie').style.height=document.getElementById('movie').scrollWidth*0.8+'px'</script>
&emsp;&emsp;LPS的计算搞清楚后，我们来看KMP算法本身，现在假设在下面的Text中寻找Pattern子字符串。
![leetcode26_09](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_09.png)  
&emsp;&emsp;我们可以发现，除掉最后一个Y，所有的pattern字符串都匹配上了，这个也就意味着在pattern的'Y'之前的6个字符组成的字符串"BCDABC"是与**text中在'X'之前的6个字符组成的字符串**"BCDABC"匹配（Y之前一共有7个字符），如下图。
![leetcode26_10](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_10.png)  
&emsp;&emsp;在暴力解法里面，我们是向右移动一位，然后进入下图状态，现在我们想做这么一个事儿，将pattern中的前6个字符组成的字符串"ABCDAB"和与其位置对应的**text中'X'之前的6个字符组成的字符串**"BCDABC"进行比较。  
![leetcode26_11](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_11.png)  
&emsp;&emsp;我们知道在pattern字符串里面它的前6个字符组成的字符串"ABCDAB"和pattern的'Y'之前的6个字符组成的字符串"BCDABC"是不相等的，并且我们已经知道，pattern的'Y'之前的6个字符组成的字符串是与**text中在'X'之前的6个字符组成的字符串**匹配的，所以自然可以知道对于pattern中的字符串"ABCDABC"，它的longest prefix suffix长度，肯定不是6，所以向右移动一个字符肯定是不会match的。
![leetcode26_12](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_12.png)  
&emsp;&emsp;为了更好的理解这个概念，我们这里再举另外一个例子，下图我们用一样的逻辑，可以知道"AAAAAAA"的LPS是6，所以将pattern向右移动一个字符是有用的。
![leetcode26_13](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_13.png)  
&emsp;&emsp;回到刚才的例子，我们已经得出的结论是，我们首先查看不同点之前的子串，也就是"ABCDABC"，它的LPS并不是6，所以将pattern向右移动一个字符没有任何意义。
![leeetcode26_14](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_14.png)
&emsp;&emsp;类似，对于相同的子串，我们发现，如果将pattern向右移动两位，pattern的'Y'之前的5个字符"CDABC"与text的'X'之前的5个字符是匹配的，现在在来比较pattern的前5个字符组成的字符串，显然同一个子串"ABCDABC"，它的LPS也不是5，所以向右移动两个字符没有意义。
![leetcode26_14](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_15.png)  
&emsp;&emsp;同样的，向右移动三个字符也没有意义。
![leetcode26_14](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_16.png)  
&emsp;&emsp;那向右移动四个字符呢？这个时候，正好我们的"ABCDABC"的LPS就是3，所以向右移动四个字符是有意义的，而这个时候，由于三个"ABC"都互相相同，所以pattern的"ABC"和text对应位置的"ABC"是没有必要再比较了，直接从后面的第4个字符开始比较，而这个时候，text的第4个字符是'X'，pattern的第4个字符是'D'，比较这两个字符是否相等。   
![leetcode26_14](http://ovwkcbdpf.bkt.clouddn.com/image/leetcode26/leetcode26_17.png)  
&emsp;&emsp;我们可以将上面的经验总结为下面这句话，对于已经匹配了的pattern中的字符串，如果LPS是K，那么我们可以跳过pattern的前'K'个字符的匹配，然后从下标为K的

#### Code


#### Time Complexity

O(n);