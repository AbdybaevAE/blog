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

Another example:

There is an **undirected** graph with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array `graph`, where `graph[u]` is an array of nodes that node `u` is adjacent to. More formally, for each `v` in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:

- There are no self-edges (`graph[u]` does not contain `u`).
- There are no parallel edges (`graph[u]` does not contain duplicate values).
- If `v` is in `graph[u]`, then `u` is in `graph[v]` (the graph is undirected).
- The graph may not be connected, meaning there may be two nodes `u` and `v` such that there is no path between them.

A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that **every** edge in the graph connects a node in set `A` and a node in set `B`.

Return `true` *if and only if it is **bipartite***.

Problem can be found [here.](https://leetcode.com/problems/is-graph-bipartite/)

*Algorithms will be next*:

1. Create integer colors array(<code>0 = not colored vertex, 1 - first group vertex, -1 - second group vertex</code>)
2. Iterate through graph:
   1. If vertex was colored, it means we have already checked all its' adjacent vertices, just <code>continue</code> iteration
   2. Color vertex and create a queue
   3. Add vertex to queue and start cycle while queue is not empty 
      1.  Poll vertex from queue and check all its' adjacent vertices 
         1. If adjacent vertex is colored with same color then it's not bipartite graph
         2. If vertex is not colored yet, color it with opposite color and add current vertex to queue

*Why we need to iterate through all graph in second step?*

>  Graph could be not connected, that is why we need to check all its' components

Solution: 

{% github_include AbdybaevAE/data-blog/master/template-java/2.java java %}