---
title: Data Structures | Binary Search Tree
date: 2021-02-05 03:38:54
tags:
---

In this article we will talk about **Binary Search Tree.**

*What is the binary search tree?*

Node based data structure with following properties:

- The left subtree of node contains values that are lesser than node's value
- The right subtree of node contains values that are bigger than nodes' value
- Left and right subtrees are also binary search trees.

*Which operations we can peform on binary search trees?*

- Insert value
- Get minimum value
- Get maximum value
- Search value
- Get height of tree
- Delete value

*Are they contains duplicates?*

No

*What about asymptotic complexity of operations?* 

Depends on "balance" property. In balanced trees - logarithmic complexity, in unbalanced trees - linear complexity. 

*What about space complexity?* 

Linear complexity

*What about insert operation?*

{% github_include AbdybaevAE/data-blog/master/bst/6.java java %}

If tree is empty then define root with value val, otherwise insert recursively into tree, until we find suitable place.`insertRecursively` function search for suitable place, if there is some insert new node and return newely created node, otherwise search suitable place in children's subtrees and return given current node.

*What about get maximum, minimum value operation?*

{% github_include AbdybaevAE/data-blog/master/bst/7.java java %}

As we know each node's right children is bigger than current node, so the most biggest node is rightmost.

The same logic for minumum operation: 

{% github_include AbdybaevAE/data-blog/master/bst/8.java java %}

*What about search operation?* 

{% github_include AbdybaevAE/data-blog/master/bst/9.java java %}

*What about height operation?* 

{% github_include AbdybaevAE/data-blog/master/bst/11.java java %}

*What about delete operation?*

{% github_include AbdybaevAE/data-blog/master/bst/12.java java %}

If node do not present in tree, so nothings happens. 

If deleting node has one child then return that child(change refference of node's parent child to node's child)

If deleting node has two childrens then find the smallest value in right subtree, setup that value to current node's value and recursively delete smallest node. 

