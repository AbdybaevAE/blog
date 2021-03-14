---
title: Dynamic Programming | Practise 3
date: 2021-03-14 19:06:58
tags:
---

In this article we talk about **dynamic programming.**

Lets look at next question: 

Given two strings `str1` and `str2`, return the shortest string that has both `str1` and `str2` as subsequences. If multiple answers exist, you may return any of them.

*(A string S is a subsequence of string T if deleting some number of characters from T (possibly 0, and the characters are chosen anywhere from T) results in the string S.)*

 

**Example 1:**

```
Input: str1 = "abac", str2 = "cab"
Output: "cabac"
Explanation: 
str1 = "abac" is a subsequence of "cabac" because we can delete the first "c".
str2 = "cab" is a subsequence of "cabac" because we can delete the last "ac".
The answer provided is the shortest such string that satisfies these properties.
```

 

**Note:**

1. `1 <= str1.length, str2.length <= 1000`
2. `str1` and `str2` consist of lowercase English letters.

The problem can be found [here.](https://leetcode.com/problems/shortest-common-supersequence/) 

Problem very tricky and need some investigation. One of solutions could be dynamic programming approach. 

You can come up with next statement: longest common subsequence of this two strings will be added to final answer only once. And another left chars must be added by order in which they appear from two strings. So, algorithm will be next: 

1. Find longest common subsequence
2. Add indexes of chars in longest common subsequence to list
3. Traverse both strings simultaneously and added each chars from strings to final answer, if char is char from longest common subsequence, then add this char once 

Solution:

{% github_include AbdybaevAE/data-blog/master/template-java/3.java java %}

Notes: 

1. Declare cache array of lonest common subsequence
2. From line 3 to 13 find the lenths of longest common subsequence
3. From line 15 to 25 find indexes of chars of longest common subsequence
4. From line 29 to 44 traverse strings and add chars from to answer following rules from step 3 in algorithm
5. On lines 45 and 46 add left chars


