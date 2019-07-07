---
layout: post
author: smi
date: 2019-07-07 08:00:00 +0200
categories: pharo
title: Binary Search Tree in Pharo
comments: true
---



Second phase of  [GSoC 2019](<https://summerofcode.withgoogle.com/>) coding period on [Pharo](<http://pharo.org/>) project is about implementing tree data structures. This week I've been working on implementing Binary Search Tree.

Consulting with mentors we have decided to start implementing trees as composite data structure also known as rooted trees. This means that a tree consists of nodes and each node has a key field and references to child nodes.  Also we were talking about having the same interface for all different trees. The idea is to just start implementing them and in time the common methods will crystallize into an interface.

## Binary Tree

The journey has begun with Binary Tree.  A simple BinaryTree class:

```
Object subclass: #BinaryTree
	instanceVariableNames: 'root'
	classVariableNames: ''
	package: 'Containers-BinaryTree'
```

that holds reference to its root node. Node class was represented as:

```
Object subclass: #BinaryNode
	instanceVariableNames: 'key leftChild rightChild'
	classVariableNames: ''
	package: 'Containers-BinaryTree'
```

 with getters and setters for each field and a method that checks if the tree is empty (if the root is nil).

Binary tree has two basic structural characteristics:

* size - number of nodes in a tree
* depth

#### Depth

Depth of a binary tree can be calculated as length of the longest path from a node to the root. For each node in a binary tree there is exactly one path from a node to the root.

If a tree has only one node its depth is 0 and if tree has no nodes (is empty) its depth is -1.

```
BinaryTree >> depth
	"Depth of a binary tree is length of longest path from an arbirary node to a root. It the three is empty the depth is -1. If a three only has a root element its depth is 1 "
	self isEmpty 
	ifTrue: [ ^-1 ].
	^self depth: self root.
```

```
depth:aNode
	"Returns depth of a tree starting from the given node"
	| leftDepth rightDepth |
	leftDepth := -1.
	aNode leftChild isNotNil 
	ifTrue: [ leftDepth := self depth: aNode leftChild ].
	rightDepth := -1.
	aNode rightChild isNotNil 
	ifTrue: [ rightDepth := self depth: aNode rightChild ].
	
	( leftDepth > rightDepth )
	ifTrue: [ ^ (1 + leftDepth) ]
	ifFalse: [^ (1 + rightDepth ) ].
```



#### Size

Size of a tree represents number of nodes in a tree. An empty tree has a size of 0.

```
size
	"Returns size of a tree - number of nodes in a tree"
	self root isNil 
	ifTrue: [ ^0 ].
	^self size: self root.
```

```
size:aNode
	"returns size of a tree starting from a given node"
	| leftSize rightSize |
	leftSize := 0.
	rightSize := 0.
	aNode leftChild isNotNil 
	ifTrue: [ leftSize := (self size: (aNode leftChild)) ].
	aNode rightChild isNotNil
	ifTrue: [ rightSize := (self size: (aNode rightChild ) )].
	^ 1 + leftSize + rightSize.
```



#### Searching for an element in a tree

Two of the most common search algorithms used in trees are:

* Breath first search (bfs)
* Depth first search (dfs)

**BFS**

```
bfs: info
	"Breadth fisrt search for an information. If there is no key containing given infomration returns nil. If the info is found returns a node containing it"
	| queue |
	self isEmpty 
	ifTrue: [ ^nil ].
	queue := LinkedList new.
	queue addLast: self root.
	
	[ queue isNotEmpty ] whileTrue: [ 
		| node |
		node := queue removeFirst.
		node key == info  
		ifTrue: [ ^node ].
		node leftChild isNotNil 
		ifTrue: [ queue addLast: node leftChild ].
		node rightChild isNotNil
		ifTrue: [ queue addLast: node rightChild ].
		 ].
		^nil.
```

**DFS**

```
dfs: info
	"Depth fisrt search for an information. If there is no key containing given infomration returns nil. If the info is found returns a node containing it"
	self isEmpty 
	ifTrue: [ ^nil ].
	^self dfs: info node: self root.
```

```
dfs: info node: aNode
	| node |
	aNode key == info
		ifTrue: [ ^ aNode ].
		
	aNode leftChild isNotNil
		ifFalse: [ ^ nil ].
	node := self dfs: info node: aNode leftChild.
	node isNotNil
		ifTrue: [ ^ node ].
		
	aNode rightChild isNotNil
		ifFalse: [ ^ nil ].
	node := self dfs: info node: aNode rightChild.
	node isNotNil
		ifTrue: [ ^ node ].
```



Further discussion with mentors lead to turning Binary Tree into a Binary Search Tree.

## Binary Search Tree

[Binary search trees](https://en.wikipedia.org/wiki/Binary_search_tree) are a type of binary trees  with special properties:

* All nodes are unique - there are no duplicates
* For each node all nodes that have greater value are contained in a right subtree and all nodes that have lesser values are contained in left subtree

![Binary Search Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/450px-Binary_search_tree.svg.png)



Key methods to be implemented are:

* adding new element
* removing an element



#### Adding new element

```
add:aKey
	"Add a node with passed key to a binary search tree"
	self isEmpty
	ifTrue: [^(self root: (self add: aKey node: self root ))].
	 ^ self add: aKey node: self root
```

```
add: aKey node: aNode
	"Add a node with passed key to a binary search tree"

	aNode isNil
		ifTrue: [ ^ (BinaryNode new key: aKey) ].
	aKey < (aNode key)
		ifTrue: [ ^(aNode leftChild: (self add: aKey node: aNode leftChild)) ].
	aKey > (aNode key)
		ifTrue: [ ^(aNode rightChild: (self add: aKey node: aNode rightChild))].
	aKey == (aNode key)
		ifTrue: [self error: 'key already exists'].
```



Next few methods to be implemented:

* removing an element from a binary search tree

* traversals:  pre-order, in-order, post-order

* etc. 

  

## Testing

It is important for all code to be tested and as much use cases as possible. Most of these methods were tested for 3 cases:

* does the method work if the tree is empty
* does the method work for leftChild
* does the method work for a rightChild

Binary Search Trees are specific and the fact that keys are unique should also be tested.

What I learned is that writing methods comments usually helps in determining which use cases should be tested.

## Next steps

Execution time and memory should be measured to check if this implementation is optimal for Pharo.

After Binary Trees different types of balancing trees need to be implemented. 



#### Image reference: 

Image presented in this post is taken from Wikipedia. Links is provided in-text. 

