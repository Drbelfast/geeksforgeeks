---
title: A&DS-Threaded Binary Tree
date: 2016-08-05 22:21:58
tags:
categories: Algorithm
---

A **Threaded binary tree** is a binary tree variant which allows **fast traversal**: given a pointer to a node in a threaded, it is possible to *cheaply* find its in-order successor.

## Motivation

For normal simple Binary search tree, if we want to know the ordering, a recursive traversal algorithm could be applied.

```java
Algorithm: traverse(t):
 1. input: a pointer t to a node (or nil)
 2. if t = nil, return
 3. else:
    - traverse(left-child(t))
    - visit t
    - traverse(right-child(t))
```

The problem is it uses stack space proportional to the height of a tree. which is O(log N) for fairly balanced, and O(n) for worst case chaining.

> In 1968, [Donald Knuth](https://en.wikipedia.org/wiki/Donald_Knuth) asked whether a non-recursive algorithm for in-order traversal exists, that uses no stack and leaves the tree unmodified. One of the solutions to this problem is tree threading, presented by J. M. Morris in 1979. (to make inorder traversal faster withouth recursion without stack)

## Definition

Types of threaded:

1. Single threaded: where a NULL right pointers is made to point to the inorder successor(if successor exists).
2. Double threaded: where both left and right NULL pointers are made to point to inorder predecessor and inorder successor respectively. The predecessor threads are useful for reverse inorder traversal and postorder traversal.

<img src="/images/threadedbinarytree.png" alt="Double Threaded Binary Tree" width="300"/>




## Convert a binary tree to Threaded binary tree
### Convert a binary tree to single threaded binary tree
1. Using a queue to store inorder nodes. And traverse again, set the nodes whose right child is null to the queue.peek().
  Time complexity O(N), space complexity O(N). [detailed code](http://www.geeksforgeeks.org/convert-binary-tree-threaded-binary-tree/).
2. Using Morris Traversal. Time complexity O(N), space complexity O(1).



## Reference:

1. [Threaded binary tree @ wiki](https://en.wikipedia.org/wiki/Threaded_binary_tree)

2. [Threaded binary tree @geeksforgeeks](http://quiz.geeksforgeeks.org/threaded-binary-tree/)

3. [Convert a Binary Tree to Single Threaded binary tree](http://www.geeksforgeeks.org/convert-binary-tree-threaded-binary-tree/), introduces a way to convert binary tree to a single threaded binary tree.

4. [Threaded Binary Tree @youtube](https://www.youtube.com/watch?v=HFbA0klBKIg)

   ​