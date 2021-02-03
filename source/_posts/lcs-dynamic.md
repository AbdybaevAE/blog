---
title: LCS Dynamic Programming
date: 2021-02-01 16:57:05
tags:
---

In this article we will talk about Longest Common Sunsequence. 
Given next problem:
*Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, where in each step you can delete one character in either string.*

```txt
Example
Input: "sea", "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```

Intuitively we get recursive solution. Lets define next function:

```java
int lcs(String s1, String s2, int n1, int n2) 
```

Function returns the common longest subsequence for strings s1 and s2 with corresponding length n1 and n2.

1. Base case would be when n1 or n2 equals to zero, in this case longest common subsequence of empty and not empty strings would be empty string. Return value would be <code>0</code>.
2. There are two cases exists:
   1. <code>s1.charAt(n1 - 1) == s2.charAt(n2 - 1).</code> In this case we know that given strings of size n1 and n2 has two same chars at positions n1 - 1 and n2 - 1. And all we need to do is to find common subseqence of strings n1 - 1, n2 - 1. Return value would be <code>1 + lcs(s1, s2, n1 - 1, n2 - 1)</code>
   2. <code>s1.charAt(n1 - 1) != s2.charAt(n2 - 1).</code>In this case we can conlcude that common subsequence could end at index n1 - 1 or n2 - 1. That is why we need to check both cases and select maximum common subsequence. Return value would be <code> Math.min(lcs(s1,s2,n1,n2-1), lcs(s2,s2,n1-1,n2);</code>

Lets combine this into one function:

```java
    public static int lcs(String s1, String s2, int n1, int n2) {
        if (n1 == 0 || n2 == 0) return 0;
        if (s1.charAt(n1-1) == s2.charAt(n2-1)) {
            return 1 + lcs(s1,s2, n1-1, n2-1);
        } else {
            return Math.max(lcs(s1,s2,n1-1,n2),lcs(s1,s2,n1,n2-1));
        }
    }
```

Keep in mind: we need substract double length of lcs from sum of length of strings. Because the statement is to find minimum number of chars to delete to get equal strings. 

```java
package com.company;

public class Main {
    public static void main(String[] args) {
        String s1 = "sea", s2 = "eat";
        System.out.format("Ans is %d", minDelete(s1,s2));
    }
    public static int minDelete(String s1, String s2) {
        int n1 = s1.length(), n2 = s2.length();
        return n1 + n2 - 2 * lcs(s1,s2,n1,n2);
    }
    public static int lcs(String s1, String s2, int n1, int n2) {
        if (n1 == 0 || n2 == 0) return 0;
        if (s1.charAt(n1-1) == s2.charAt(n2-1)) {
            return 1 + lcs(s1,s2, n1-1, n2-1);
        } else {
            return Math.max(lcs(s1,s2,n1-1,n2),lcs(s1,s2,n1,n2-1));
        }
    }
}
```

Let's optimize algorithm. Recursion calls itself again and again, and instead of getting values from recursion we can cache answers and use it later. Cache would be simple two dimensional array of size n1 + 1, n2 + 1, that holds Integers. If `cache[i][j] != null` then cache holds precomputed value, otherwise compute and update cache.
```java
    public static int minDelete(String s1, String s2) {
        int n1 = s1.length(), n2 = s2.length();
        Integer[][] cache = new Integer[n1 + 1][n2 + 1];
        return n1 + n2 - 2 * lcs(cache, s1,s2,n1,n2);
    }
    public static int lcs(Integer [][] cache, String s1, String s2, int n1, int n2) {
        if (cache[n1][n2] != null) return cache[n1][n2];
        if (n1 == 0 || n2 == 0) return 0;
        int ans;
        if (s1.charAt(n1-1) == s2.charAt(n2-1)) {
            ans = 1 + lcs(cache, s1,s2, n1-1, n2-1);
        } else {
            ans = Math.max(lcs(cache, s1,s2,n1-1,n2),lcs(cache, s1,s2,n1,n2-1));
        }
        return cache[n1][n2] = ans;
    }
```

We can break algorithm if we provide big strings that gives overflow of stack. It has place to make iterative solution. The idea remains the same. If current chars `i, j` are same we have got new longest subsequence at path `cache[i][j]`, if not then the answer would be the biggest value between `cache[i][j-1]` and `cache[i-1][j]`(don't forget to change `Integer[][]cache -> int[][]cache`).

```
public static int lcs(int [][] cache, String s1, String s2, int n1, int n2) {
    for (int i = 0; i <= n1; ++i) {
        for (int j = 0; j <= n2; ++j) {
            if (i == 0 || j == 0) continue;
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                cache[i][j] = 1 + cache[i-1][j-1];
            } else {
                cache[i][j] = Math.max(cache[i][j-1], cache[i-1][j]);
            }
        }
    }
    return cache[n1][n2];
}
```

 