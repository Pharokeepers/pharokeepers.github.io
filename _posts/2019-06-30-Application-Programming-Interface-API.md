---
layout: post
author: smi
date: 2019-06-30 08:00:00 +0200
categories: pharo
title: Tree Application Programming Interface (API)
comments: true
---



[An application programming interface (API)](https://en.wikipedia.org/wiki/Application_programming_interface#Design) is a set of clearly defined methods of communication between different components of a system. API simplifies program development by abstracting the underlying implementation and exposing only objects and methods the user needs, while hiding the details of implementation and parts of the system that are subject to change. In this blog post we look at designing an API for several basic tree data structures. 



# API implementation

API usually describes the desired behavior of a software library, and may have multiple implementations (i.e. different software libraries have same API). API can also include a specification of classes and class methods. The idea of an API is to hide the implementation complexity and  may have a huge impact on software adoption and usage. A well designed API can significantly speed up program development. 

The most important building block of tree data structures is the **tree node**. A tree node consists of:

* Data value 
* An array of references to the child nodes 
* Reference to the parent node

As we are primarily interested in [binary trees](https://www.geeksforgeeks.org/binary-tree-data-structure/), a tree node will usually contain an array of two elements - the so called left (at position 0) and right (at position 1) child node, but it should be possible to have an arbitrary number of children. 

Common methods supported by the tree node include:

* return number of children
* return child at some position *i*
* get index of node *n* in the children array
* return parent node
* check if the node has any children (i.e. is a leaf node)
* Add a child node at position *i*
* Delete a child node at position *i*

A **tree data structure**, contains a reference to the root node, which is *nil* if the tree is empty.  Two of the basic operations which will be used by other methods are the method to return a subtree given a node *n* (i.e. return a tree that has the node *n* as a root), and the tree traversal. Tree is usually traversed in 

* breadth first (aka level order) or 
* depth first order
  * Inorder: left - root -right
  * Preorder: root - left - right
  * Postorder: left -right -root

Other common operations include [adding](https://www.geeksforgeeks.org/insertion-in-a-binary-tree-in-level-order/) and [deleting](https://www.geeksforgeeks.org/deletion-binary-tree/) nodes. When adding nodes, we usually do iterative level order traversal and for each node check if there is an empty child node (from left to right). When we find an empty child node, we add the new node at this position. When deleting a node we will use the following [algorihtm](https://www.geeksforgeeks.org/deletion-binary-tree/):

1. Starting at root, find the deepest and rightmost node in binary tree and node which we want to delete.
2. Replace the deepest rightmost node’s data with node to be deleted.
3. Then delete the deepest rightmost node.

This way, the tree shrinks from the bottom when deleting a node. 

Other common methods supported by trees should include:

* Find a node with a given value
* Find maximum and minimum value in the tree
* Construct a tree from a given traversal
* Construct a [doubly chained tree](https://pharokeepers.github.io/pharo/2019/06/23/Left-Child-Right-Sibling.html) given a general *m-ary* tree. 
* Construct an *m-ary* tree given a doubly chained tree.
* Convert a binary tree to a linked list
* Sum all nodes with some property (e.g. left/right leaves, have same parent ... )
* Merge two trees

* Print trees 
* ...

The following [link](https://www.geeksforgeeks.org/binary-tree-data-structure/) contains a list of different tree-based algorithms that will be used as a guide for implementing the tree data structure.

These data structures represent simple trees. Other tree data structures such as different self-balancing trees and quad trees will be implemented based on the simple trees. 



