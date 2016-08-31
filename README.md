## Divide and Conquer

1. [Merge sort](https://github.com/Drbelfast/geeksforgeeks/blob/master/mergesort.md)
2. [Quick sort]()

### Exercise

1. [Power(x,n)]()
2. [Median of two sorted array]()
3. [Count inversions]()
4. [Closest pair of points]()


## Binary Tree

[Binary Tree]()

### Balanced binary search tree

1. [AVL tree]()

2. [2 3 tree]()
3. [Red black tree]()
4. [Difference between AVL tree and Read black tree]()

### Threaded Binary Tree

1. [Introduction to Threaded Binary Tree]()
2. [Single Threaded Binary Tree implementation]()
3. [Double Threaded Binary Tree implementation]()
4. [Convert BST to Threaded Binary Tree]()

### Exercise

1. Add all greater values to every node in a given BST](http://www.geeksforgeeks.org/add-greater-values-every-node-given-bst/)

   就是一个reverse inorder traversal.

2. [Remove BST keys outside the given range](http://www.geeksforgeeks.org/remove-bst-keys-outside-the-given-range/)

   用postorder traversal 把 child 都处理完了，再看当前node节点， 相当于bottom up

3. [Check if each internal node of a BST has exactly one child](http://www.geeksforgeeks.org/check-if-each-internal-node-of-a-bst-has-exactly-one-child/)

   如果存在两个child node，当前数字与最后一位数字之差  肯定和 当前数字与下一位数字之差 不同符号。


4. [Find if there is a triplet in a Balanced BST that adds to zero](http://www.geeksforgeeks.org/find-if-there-is-a-triplet-in-bst-that-adds-to-0/)
   1. 如果用inorder traversal 把结果存储在一个array里面 就跟 3sum是一样的了。

      时间复杂度是O(N^2), 空间复杂度是O(N)。

      但是题目要求 空间复杂度是O(logN)

   2. 转换成double linked list. 这样就不需要额外空间了。

5. [Merge two BSTs with limited extra space](http://www.geeksforgeeks.org/merge-two-bsts-with-limited-extra-space/)

6. [Two nodes of a BST are swapped, correct the BST]()

7. [Contruct BST from given preorder traversal Set 1]()

8. [Construct BST from given preorder traversal Set 2]() 

9. [Floor and Ceil from a BST]()

   ​


## Heap

1. [Heaps]()



## Graph

1. [Kruscal's algorithm]()
2. [Prim's algorithm]()
3. [Dijskstra's algorithm]()
4. [Boyer Moore]()
5. [Topogolical sort]()

## String Pattern

1. [KMP]()
2. ​