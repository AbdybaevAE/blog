---
title: Algorithms | Knuth–Morris–Pratt algorithm
date: 2021-04-24 17:48:43
tags:
---

In this article we talk abount KMP algorithm

**Let's define a statement:**

Find all occurrence of pattern in string. 

By using naive approach we get answer of <code>O(m * n)</code> complexity, where  <code>n</code> - length of text and <code>m</code> - length of pattern. However applying KMP algorithm, this could be done of <code>O(m + n)</code> asymptotic complexity and <code>O(m)</code> space complexity. 

Algorithm:

{% github_include AbdybaevAE/algos/main/algos/Kmp.java java %}

Main idea is next:

1. Pre compute longest proper prefix which is also suffix(<code>lps</code>)
2. Define <code>textIndex, patternIndex</code> as iteration values in cycle
3. Iterate in text and do comparison between corresponding indexes of text and pattern:
   1. If match case, increment both indexes of text and pattern
   2. In case when index of pattern equals to lenth of pattern, it means we finded a match
   3. In another case decrement corresponding index of pattern until we find a match or it will become a zero. In zero case increment text index

 