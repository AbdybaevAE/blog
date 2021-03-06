---
title: Breadth First Search | Practise 1
date: 2021-03-06 20:12:48
tags:
---

In this article we talk about **Breadth-first search.**

The main difference between **BFS** and **DFS** is solving approach. BFS uses <code>Queue</code> to solve problem while DFS uses <code>Stack</code>.  BFS grows equally by processing closest points while DFS go deep as much as possible on each iteration. We can get that by using <code>Queue</code> and <code>Stack</code>. 

Let's look at problem: 

You are given an `m x n` `grid` where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return *the minimum number of minutes that must elapse until no cell has a fresh orange*. If *this is impossible, return* `-1`.

Problem can be found [here.](https://leetcode.com/problems/rotting-oranges/)

To solve this problem we can use BFS:

1. Create <code>Queue</code> that will hold rotten oranges. Add all rotten oranges to this queue 
2. Iterate in cylce while queue is not empty and do next:
   1. Poll rotten orange from queue
   2. Check sorrounding oranges for fresh one. If there is then rotten orange and add to queue
3. Check if all fresh oranges become rotten 

Solution: 

{% github_include AbdybaevAE/data-blog/master/template-java/1.java java %}