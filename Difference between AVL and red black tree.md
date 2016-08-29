- AVL trees are more rigidly balanced and hence provide faster look-ups. Thus for a look-up intensive use an AVL tree
- For an insert intensive task, use a Read-Black tree
- AVL tree store the balance factor at each ndoe. This takes `O(N)`  extra space. However, if we know that the keys that will be inserted in the tree will always be greater than zero, we can use the sign bit of the keys to store the colour information of a red-black tree. Thus, in such cases red-black tree takes `O(1)` extra space.
- In general, the rotation for an AVL tree are harder to implement and debug than Red-Black tree

Red-black trees are more general purpose. They do relatively well on add, remove, and look-up but AVL trees have faster look-ups at the cost of slower add/remove. Red-black tree is used in the following:

- Java: java.util.TreeMap , java.util.TreeSet .
- C++ STL: map, multimap, multiset.
- Linux kernel: completely fair scheduler, linux/rbtree.h




Take this with a pinch of salt:

B-tree when you're managing more than thousands of items and you're paging them from a disk or some slow storage medium.

RB tree when you're doing fairly frequent inserts, deletes and retrievals on the tree.

AVL tree when your inserts and deletes are infrequent relative to your retrievals.




## Reference

[stackoverflow](http://stackoverflow.com/questions/13852870/red-black-tree-over-avl-tree)

