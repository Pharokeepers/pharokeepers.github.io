---
layout: post
author: smi
date: 2019-08-19 08:00:00 +0200
categories: pharo
title: M-ary trees
comments: true
---

[M-ary tree](https://en.wikipedia.org/wiki/M-ary_tree) is a tree data structure in which each node has no more than m children. I have already mentioned M-ary trees in an [earlier blog post](https://pharokeepers.github.io/pharo/2019/06/15/SmiljanaRootedTrees.html). I've also written about the [left child right sibling](https://pharokeepers.github.io/pharo/2019/06/23/Left-Child-Right-Sibling.html) representation. In this blog post I want to write about M-ary trees in greater detail.



## Introduction

M-ary tree is a generalization of a binary tree, where every node has M or less children (i.e. binary tree is an M-ary tree, with M = 2). Following [image](https://www.geeksforgeeks.org/number-of-paths-of-weight-w-in-a-k-ary-tree/) shows an example of an M-ary tree, with M = 3.

![](https://media.geeksforgeeks.org/wp-content/uploads/tree-1-1-300x200.jpg)



If every node of an M-ary tree has either M or 0 children, then the tree is called a **full** M-ary tree. If every leaf node of a full M-ary tree is at the same depth, the tree is said to be **perfect**. If all levels except the last one are full (i.e. every non-leaf node has M children), the tree is said to be **complete**. 



## Traversal

Similarly as with binary trees, we have: 

* Pre-order traversal - visit a node and then traverse the subtrees rooted at its children (one at a time) going from left to right. 
* Post-order traversal - recursively traverse all subtrees rooted at the children (starting from left to right) first and then visit the root node.
* In-order traversal - traverse the left subtree, visit the root node and then traverse the right subtree.

In order to do the in-order traversal we must first define the notion of *left* and *right* subtree.  [Standard way of doing this](https://en.wikipedia.org/wiki/M-ary_tree#Traversal_methods_for_m-ary_trees), when having M > 2 children, is to divide the list of child nodes into two non-overlapping groups which will constitute the left and the right subtree.

* left subtree: ![](http://mathurl.com/render.cgi?%5Cleft%5C%7B0%2C1%2C%20%5Cdots%20%5Cleft%5Clfloor%5Cfrac%7BM%7D%7B2%7D%5Cright%5Crfloor%20%5Cright%5C%7D%5Cnocache)
* right subtree:  ![](http://mathurl.com/render.cgi?%5Cleft%5C%7B%5Cleft%5Clceil%5Cfrac%7BM%7D%7B2%7D%5Cright%5Crceil%20%5Cdots%20M%5Cright%5C%7D%5Cnocache)



## Applications

M-ary trees have many applications which include:

1. Represent a file system data structure (with nodes representing files or folders).
2. Parse and grammar trees for natural language processing applications
3. Abstract syntax trees for representing the structure of a program code.
4. Use in image processing and mesh generation
5. Use in game engines for rendering and collision detection
6. Color quantization
7. and many more...



[Following image](https://www.nltk.org/book/tree_images/ch08-tree-2.png) shows an example of a grammar tree. 



![](https://www.nltk.org/book/tree_images/ch08-tree-2.png)



[The following](https://en.wikipedia.org/wiki/Octree) image shows an octree (M = 8) used for 3D rendering.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/Octree2.svg/1599px-Octree2.svg.png)



## Conclusion 

General M-ary trees have many applications, ranging from computer science and compiler design to 2D/3D image processing and rendering. It is very important to have a general M-ary tree data structure in Pharo to be used as a starting point for building interesting projects in different areas. 