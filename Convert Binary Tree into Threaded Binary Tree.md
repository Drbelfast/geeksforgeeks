---
title: Convert Binary Tree into Threaded Binary Tree
date: 2016-08-24 22:21:58
tags:
categories: Algorithm
---
## Convert to Single Threaded Binary Tree
### Solution 1
we can do the inorder traversal and store it in some queue. Do another inorder traversal and where ever you find a node whose right reference is NULL, take the front element from the queue and make it the right of the current node.

### Better Solution
```java

public class BSTtoTBST {

    public static Node root;

    public void convert(Node root){
        inorder(root, null);
    }

    public void inorder(Node root, Node previous){
        if(root==null){
            return;
        }else{
            inorder(root.right, previous);
            if(root.right==null &&  previous!=null){
                root.right = previous;
                root.rightThread=true;
            }
            inorder(root.left, root);
        }
    }

    public void print(Node root){
        //first go to most left node
        Node current = leftMostNode(root);
        //now travel using right pointers
        while(current!=null){
            System.out.print(" " + current.data);
            //check if node has a right thread
            if(current.rightThread)
                current = current.right;
            else // else go to left most node in the right subtree
                current = leftMostNode(current.right);
        }
        System.out.println();
    }

    public Node leftMostNode(Node node){
        if(node==null){
            return null;
        }else{
            while(node.left!=null){
                node = node.left;
            }
            return node;
        }
    }

    public static void main(String[] args) {
        root = new Node(10);
        root.left = new Node(5);
        root.right = new Node(15);
        root.left.left = new Node(1);
        root.left.right = new Node(7);
        root.right.left = new Node(12);
        root.right.right = new Node(20);

        BSTtoTBST bsTtoTBST = new BSTtoTBST();
        bsTtoTBST.convert(root);
        System.out.println("Inorder Traversal: ");
        bsTtoTBST.print(root);
    }
}

class Node{
    Node left;
    Node right;
    int data;
    boolean rightThread;
    public Node(int data){
        this.data = data;
        rightThread = false;
    }
}
```

## Convert to Double Threaded Binary Tree

## Convert to Double linked list
```java
public static void convertToDoubleLinkedList(Node root) {
        ArrayList<Node> res = new ArrayList<Node>();
        res.add(null);
        inOrder(root, res);
    }
    
    public static void inOrder(Node root, ArrayList<Node> res) {
        if (root == null) return;
        inOrder(root.left, res);
        root.pre = res.get(0);
        if (res.get(0) != null) {
            res.get(0).suc = root;
        }
        res.set(0, root);
        inOrder(root.right, res);
    }
```

## Reference
[link](http://algorithms.tutorialhorizon.com/convert-binary-tree-into-threaded-binary-tree/)