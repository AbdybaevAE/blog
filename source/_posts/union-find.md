---
title: Data Structures | Disjoint-Set(Union Find)
date: 2021-01-31 04:29:28
tags:
---

In this article we will talk about **Union Find.**

Let's imagine that we have set of N elements, and some elements are connected. Elements that are connected produce some subset. Your question is to find number of distinct subsets or to find set with maximum number of members.

**Case #1**
*There are n cities and k connections. Connected cities(directly or indirectly) declares province. Find total number of province.*

Constraints: 

```txt
1 <= n <= 10000
arr[s] = [i,j]; 1 <= i,j <= n, i != j, [i,j] - unique pairs
```

```txt
Example #1 
Input: 
10 
[[1,2], [1,3], [2,5], [7,8], [5, 6], [9,10]]
Output: 4
```

From example above you can see that provinces are:

- 1, 2, 3, 5, 6
- 4
- 7, 8 
- 9, 10

In total we have 4 provinces. 

Efficient approach to solve this problem is to use Union Find DS. The main idea is

1. Create unique ids array for each element in set. It means if we have 10 elements in set, unique ids are nums[1,2,3,4,5,6,7,8,9,10]. 

2. Define root element. Root element is an element where nums[i] = i. Initially all elements are roots. We have 10 roots. If we have nums = [1, 1, 1, 1, 5, 5, 5, 5, 9, 10], it means root elements are 1, 5, 9, 10, moreover if we have nums = [1, 1, 1, 1, 1, 1, 5, 5, 9, 10], then root elements are 1, 9, 10 (because nums[5] =1)

3. Implement "find" function. "Find" function searches root of element.

   ```java
    public static int find(int[] nums, int i) {
         while(nums[i] != i) {
              i = nums[i];
         }
         return i;
    }
   ```

   

4. Implement union function. Union function connect to elements. How do we do this? Find root of first element(root1), find root of second element(root2). Setup nums[root1] = root2

```java
 public static void union(int[] nums, int i, int j) {
        int rootI = find(nums, i);
        int rootJ = find(nums, j);
        nums[rootI] = rootJ;
 }
```

Let's define final algorithm for the question:

1. Create unique ids array(nums)
2. Iterate through connection array and union cities 
3. Find total number of roots in nums. 

Solution:

```java
package com.company;
import java.util.HashSet;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        int n = 10;
        int [][] connections = new int [][] {{1,2}, {1,3}, {2,5}, {7,8}, {5,6}, {9,10}};
        int ans = numberOfProvince(n, connections);
        System.out.format("Number of provinces - %d", ans);
    }
    public static int find(int[] nums, int i) {
        while(nums[i] != i) {
            i = nums[i];
        }
        return i;
    }
    public static void union(int[] nums, int i, int j) {
        int rootI = find(nums, i);
        int rootJ = find(nums, j);
        nums[rootI] = rootJ;
    }
    public static int numberOfProvince(int n, int[][] connections) {
        int[] nums = new int [n + 1];
        for (int i = 1; i <= n; ++i) {
            nums[i] = i;
        }
        for (int[] conn: connections) {
            union(nums, conn[0], conn[1]);
        }
        Set<Integer> roots = new HashSet<>();
        for (int i = 1; i <= n; ++i) {
            int currRoot = find(nums, i);
            roots.add(currRoot);
        }
        return roots.size();
    }
}
```

**Case #2**

*Given an unsorted array of integers arr, find the length of longest consucutive elements sequence.* 

```txt
Example #1
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example #2
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

If you think about this problem in Union Find way, you can get that all consecutive elements sequece define some subset(connected component) and all we need to do is to find the biggest one. In general we need to iterate through array and try to union elements (val, val + 1) and (val, val - 1) if they given. It means we need to know whether there exists values (val + 1) or (val - 1) in order to retrive their indexes. This can be done via projecting values to indexes. Map would be effecient way. What happens if you have duplicates? Actually it doesn't matter, because we store only the last occurence of value in map and we need keep in mind to process indexes that are exists in map. How we can get maximum size set? We can create another array counter, that will keep track size of each root's set.

Solution: 

```java
package com.company;

import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        int [] arr = new int [] {100,4,200,1,3,2,2,2};
        int ans = longestConsecutive(arr);
        System.out.format("Longest sequence size - %d", ans);
    }
    public static int find(int[] nums, int i) {
        while(nums[i] != i) {
            i = nums[i];
        }
        return i;
    }
    public static void union(int[] nums, int i, int j) {
        int rootI = find(nums, i);
        int rootJ = find(nums, j);
        nums[rootI] = rootJ;
    }
    public static int longestConsecutive(int[] arr) {
        int n = arr.length;
        if (n == 0) return 0;
        int [] nums = new int [n];
        Map<Integer, Integer> mp = new HashMap<>();
        for (int i = 0; i < n;++i) {
            nums[i] = i;
            mp.put(arr[i], i);
        }
        for (int i = 0; i < n; ++i) {
            if (mp.get(arr[i]) != i) continue;
            int prev = arr[i] - 1, next = arr[i] + 1;
            if (mp.containsKey(prev)) {
                union(nums, i, mp.get(prev));
            }
            if (mp.containsKey(next))  {
                union(nums, i, mp.get(next));
            }
        }
        int ans = 1;
        int [] counter = new int [n];
        for (int i = 0; i < n; ++i) {
            int currRoot = find(nums, i);
            ans = Math.max(ans, ++counter[currRoot]);
        }
        return ans;
    }
}
```

Both problems can be found in leetcode.com.