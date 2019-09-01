---
layout: post
author: smi
date: 2019-08-29 08:00:00 +0200
categories: pharo
title: Trees architecture
comments: true
---





Here is [video](https://www.dropbox.com/s/8boxsz5kt1q6trq/GSOC2019_NewCollectionsInPharo_V2.mp4?dl=0&fbclid=IwAR2HE9HufkMEyEeoid85GPf2KDHV3_HdOl4UjukPUruBPE5FQAOwE08trmY) presenting my work for  [GSoC 2019](<https://summerofcode.withgoogle.com/>) with [Pharo](<http://pharo.org/>) project and a sneak peak into architecture of implemented trees.



## Binary Tree

BinaryTree was designed using several design patterns. CTAbstractTreeNode provides a common interface for CTBinaryTree and CTNullNode and is a part of Composite design pattern. CTBinaryTree represents both a node and an entire tree. It holds reference to NullNode and CTAbstractTree node. CTNullNode represents Null object pattern  (and Singleton at the same time) and provides default behavior for methods defined in CTAbstractTree. Null object represents an empty node and was introduced to reduce unnecessary `isNil` checks and make code more readable. CTGeneralTree was introduced to serve as part of a State design and holdes reference to a CTAbstractTree which was intended to be CTNullNode if the tree was empty or CTBinaryTree if it wasn't. It was also the idea that in CTAbstractTree a state from empty to non empty and vice versa would be changed when adding / removing nodes to a tree. It is still under discussion whether this extra wrapping behavior is necessary and should it be removed.



![](/images/CTGeneralTree.png)







## N-ary Tree

CTNaryTree represent an n-ary ( or m-ary ) tree. It can have more than two child nodes. Since children are represented as an OrderedCollection an empty collection represents a null node quite nicely so the CTNullNode is not used in this implementation.

![](/images/CTGeneralTreeWholePicutre.png)





## Binary Search Tree

Moving away from extra wrapping behavior represented in CTGeneralTree, Binary search tree was defined in new package. It also has a CTAbstractBinarySearchTree class serving as an interface to CTBinarySearchTree and CTNullBinaryTree. Here CTNullBinaryTree repesentes Null object pattern and again  CTBinarySearchTree is implemented as Composite.

![](/images/BinarySearchTree.png)





## AVL Tree

AVL Tree is a balanced binary search tree and as such naturally extends CTBinarySearchTree. It also uses Composite and Null object patterns. In CTAVLTree are implemented all methods concerning balancing which is changed by adding and removing nodes to a tree. 

![](/images/AVLTree.png)



## Conclusion 

The idea is to bring all this trees into a single package in the future by refining the architecture choices. Some of these trees are still under the review and their architecture could be changed. I plan to continue working on this library, hoping to add other types of trees and refine the ones implemented.