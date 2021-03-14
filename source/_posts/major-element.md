---
title: Algorithms | Major Element In Array
date: 2021-01-30 20:49:40
tags:
---

In this article we will talk about finding **majority element** in array. 

Major element is an element that apeears in array more than half of array size times.

If you think about brute force solution, you can get this by doing O(n<sup>2</sup>) time complexity, meanwhile there are exists linear complexity solution named **Moore's Voting Algorithm.**

The basic idea is simple. Setup current major element as first element in array and created variable counter with value 1. Iterate through array and increment counter by one if current value in array equals to current major element, otherwise decrement counter. If counter equals to zero, then current element in array would be a new major element and setup counter to 1. 

After end of loop count major element in array, if there are more than half of array size repetitions, that element is **major element**, otherwise there is no major element.

Algorithm:

```java
package com.company;

public class Main {

    public static void main(String[] args) {
        int [] arr = new int [] {5,5,5,1,2,3,4,5,5,55,1, 5, 5,5};
        try {
            int ans = majorElement(arr);
            System.out.format("Major element is %d", ans);
        } catch (Exception err) {
            System.err.println(err);
        }
    }
    public static int majorElement(int[] arr) throws Exception {
        if (arr == null || arr.length == 0) throw new NullPointerException();
        int n = arr.length;
        int ans = arr[0], counter = 1;
        for (int i = 1; i < n; ++i) {
            if (ans == arr[i])
                counter++;
            else
                counter--;
            if (counter == 0) {
                counter = 1;
                ans = arr[i];
            }
        }
        int count = 0;
        for (int num: arr) {
            if (num == ans)
                count++;
        }
        if (count > n / 2) return ans;
        throw new Exception("No major element");
    }

}

```


