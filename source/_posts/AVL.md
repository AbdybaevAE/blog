---
title: Trees | AVL
date: 2021-02-06 02:02:44
tags:
---

​	In this article we talk about **AVL** tree.

​	AVL is self-balanced tree, where for each node difference between height of left and right subtrees no more than 1. 

​	Whenever you insert a node into tree, you always rebalance tree. Asymptotic complexity of  insert, search, and delete operations - logarithmic complexity and linear complexity for space complexity. Let's define **balance** property of node. Balance property equals difference of height of left and right subtrees. If `|difference| <= 1`, then the node is said balanced, otherwise not balanced.

​	Whenever we peform insert operation, we need always check on balance property(of new value's ancestor). If if not balanced, then rebalance tree by rotating operation.

There are 4 rotations exists:

- Left rotation
- Right rotation
- Left-Right rotation
- Right-Left rotation

The last two is compositions of first two(with different orders).

Example of implementation of insert operation: 

{% github_include AbdybaevAE/data-blog/master/traverse/5.java java %}


