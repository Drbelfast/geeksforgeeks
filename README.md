# geeksforgeeks

## Binary Search Tree

17. [Add all greater values to every node in a given BST](http://www.geeksforgeeks.org/add-greater-values-every-node-given-bst/)

就是一个reverse inorder traversal.

18. [Remove BST keys outside the given range](http://www.geeksforgeeks.org/remove-bst-keys-outside-the-given-range/)

用postorder traversal 把 child 都处理完了，再看当前node节点， 相当于bottom up

19. [Check if each internal node of a BST has exactly one child](http://www.geeksforgeeks.org/check-if-each-internal-node-of-a-bst-has-exactly-one-child/)

如果存在两个child node，当前数字与最后一位数字之差  肯定和 当前数字与下一位数字之差 不同符号。

20. [Find if there is a triplet in a Balanced BST that adds to zero](http://www.geeksforgeeks.org/find-if-there-is-a-triplet-in-bst-that-adds-to-0/)
    1. 如果用inorder traversal 把结果存储在一个array里面 就跟 3sum是一样的了。

时间复杂度是O(N^2), 空间复杂度是O(N)。

但是题目要求 空间复杂度是O(logN)

​	2. 转换成double linked list. 这样就不需要额外空间了。

21. [Merge two BSTs with limited extra space](http://www.geeksforgeeks.org/merge-two-bsts-with-limited-extra-space/)

    用stack 在Inorder 的时候，如果遇到偏大的一个node 再push回去

22. [Two nodes of a BST are swapped, correct the BST]()