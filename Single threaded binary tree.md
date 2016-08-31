---
title: A&DS-Single Threaded Binary Tree
date: 2016-08-23 22:21:58
tags:
categories: Algorithm
---
```java
public class SingleThreadedBinaryTree {

    public static Node root;

    public void insert(Node root, int id){
        Node newNode = new Node(id);
        Node current = root;
        Node parent = null;
        while(true){
            parent = current;
            if(id<current.data){
                current = current.left;
                if(current==null){
                    parent.left = newNode;
                    newNode.right = parent;
                    newNode.rightThread = true;
                    return;
                }
            }else{
                if(current.rightThread==false){
                    current = current.right;
                    if(current==null){
                        parent.right = newNode;
                        return;
                    }
                }else{
                    Node temp = current.right;
                    current.right = newNode;
                    newNode.right = temp;
                    newNode.rightThread=true;
                    return;
                }
            }
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
        root = new Node(100);
        SingleThreadedBinaryTree st=new SingleThreadedBinaryTree();
        st.insert(root,50);
        st.insert(root,25);
        st.insert(root,7);
        st.insert(root,20);
        st.insert(root,75);
        st.insert(root,99);

        st.print(root);
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


## Reference
1. [single threaded binary tree](http://algorithms.tutorialhorizon.com/single-threaded-binary-tree-complete-implementation/)