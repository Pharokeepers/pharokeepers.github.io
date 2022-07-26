---
layout: post
author: smi
date: 2019-06-23 08:00:00 +0200
categories: pharo
title: Left Child, Right Sibling
comments: true
---



As mentioned in the [previous post](https://pharokeepers.github.io/pharo/2019/06/15/SmiljanaRootedTrees.html), every *m-ary* tree (a tree structure with at most m children, m > 2) can be represented as a binary tree by using doubly chained trees aka [child-sibling representation](https://en.wikipedia.org/wiki/Left-child_right-sibling_binary_tree). In this post I will describe this technique in greater detail, and this will serve as a starting point for implementing *m-ary* tree and other related data structures in Pharo. 



# Doubly Chained Trees

[Binary tree](https://www.geeksforgeeks.org/binary-tree-data-structure/) is a hierarchical data structure (as opposed to linear data structures, such as lists, stacks or queues) of nodes, where each node has at most two children. Each node contains: 

1. Data 
2. Reference to the left child
3. Reference to the right child

Depending on the application and implementation, a node may also contain a reference to its parent. A trivial extension of the binary to the *m-ary* case would be for a node to contain an array of references to all of its children, but this approach may waste a lot of memory (e.g. when the tree is sparse). 

Instead of holding a reference to every child node, a [better approach](https://www.geeksforgeeks.org/left-child-right-sibling-representation-tree/) is for a node to hold a reference to its first child (left) and a reference to its immediate next sibling (right).  A parent is linked only with its first child, and each child holds a reference (right) to its next sibling in line. This approach eliminates the need of knowing the number of children per node beforehand. The process of converting an *m-ary* tree to a doubly chained tree is often called the **Knuth transform**. 

The pseudo code of the Knuth transform is as follows:

```pseudocode
procedure KnuthTransform(root):
	if root = nil:
		return
	left <- KnuthTransform(root.left)
	right <- KnuthTransform(root.right)
	
	if left = nil:
		root.left <- right
		root.right <- nil
	else:
		root.left <- left
		root.left.right <- right
		root.right <- nil
	end
	
	return root	
```



[Following image](https://en.wikipedia.org/wiki/Left-child_right-sibling_binary_tree) shows a 6-ary tree (left) and an equivalent binary tree using the left-child, right-sibling representation (right). 



![Knuth Transform](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cd/N-ary_to_binary.svg/750px-N-ary_to_binary.svg.png)



As seen from the previous image, each node in the original tree, corresponds to a node in the doubly chained tree. The children of a node now form a (singly) [linked list](https://www.scaler.com/topics/linked-list/), and in order to find the *k-th* child of some node *n*, we have to traverse the list: 

```pseudocode
procedure findK(n, k):
	child <- n.left
	while k != 0 and child != nil:
		child <- child.right
		k <- k - 1
	end
	return child
```



# Advantages and Disadvantages 

In this post we introduced a way of representing *m-ary* tree structures by using binary trees. This approach saves up memory by limiting the number of references per node to two, and is easier to implement as it builds upon the binary tree data structure. On the other hand, operations like insertion, deletion and looking up children by index take a longer time because we need to traverse a linked list in order to find the right element/position, but this operation has at most an O(m) complexity (traverse all the children of a given node), which is a good trade-off. Left-child, right-sibling representation is preferable when memory is a concern and when random access of node's children is not required (rare), which makes it perfect for [implementation of heap data structures](https://en.wikipedia.org/wiki/Left-child_right-sibling_binary_tree). 



#### Image reference: 

All images presented in this post are taken from Wikipedia. All links are provided in-text. 

