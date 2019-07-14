---
layout: post
author: smi
date: 2019-07-14 08:00:00 +0200
categories: pharo
title: Restructuring Trees
comments: true
---



This week [GSoC 2019](<https://summerofcode.withgoogle.com/>)  [Pharo](<http://pharo.org/>) project was about reshaping and polishing what was done in last week. I have received a lot of feedback from my mentors and the community which were very useful and I learned a lot. It is quite cool how Pharo community is active and ready to help.

Major changes were about tree representation: going from rooted to composite.

## Rooted Tree

A rooted tree is a tree in which a particular node is distinguished from the others and called the root node as shown in picture.



![RootedTree.png](https://proofwiki.org/w/images/thumb/4/4f/RootedTree.png/300px-RootedTree.png)



This means that most algorithms that are implemented recursively have to have a special condition for dealing with the root node. We used this representation when we learned about Data structures and algorithms in faculty and it can be found in many books on the topic. 



## Composite Tree

This is a non-rooted representation that is based on application of a version of Composite design pattern. 

Composite pattern lets you treat a group of objects the same way as you would a single instance. In our case we can treat a node of a tree the same way as a subtree and consequently as an entire tree. This would let users (clients) treat nodes and compositions of nodes uniformly.

Composite design pattern usually consists of three classes: Component, Leaf and Composite.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Composite_UML_class_diagram_%28fixed%29.svg/600px-Composite_UML_class_diagram_%28fixed%29.svg.png)



In our case, with a tree, there was no need to separate node class and a tree class. A tree could be represented as a single node and all the operations that can be performed on a tree you should be able to do on a single node and vice a versa. As a result a tree could be represented with one class - Component, in a Component design pattern.





![composite_alternate.png](/home/smi/pharokeepers.github.io/images/composite_alternate.png)

## Moving the direction of implementation

Last week it was decided to go from a more general Binary Tree implementation to a Binary Search Tree and this week we went back to general implementation that will be made more specific by subclassing. 

At this point a BinaryTree class looks like:

```
Object subclass: #CTBasicBinaryTree
	instanceVariableNames: 'object parent leftChild rightChild'
	classVariableNames: ''
	package: 'Containers-BinarySearchTree'
```



Instance variable was renamed from key to object (this is still under discussion) and a pointer to parent was added. 



## Coding style

Code is being read more often than written and thus it is very important to make the code readable and to follow coding conventions of an organization. 

A lot of good coding practices for Pharo are summarized in [Pharo with Style](<https://github.com/SquareBracketAssociates/Booklet-PharoWithStyle>) booklet.  It has a  lot of examples of what are considered to be good and bad practices for Pharo. Some of them weren't that obvious to me before I read the book.

My attention was drawn to styling mistakes I've made in the previous week and I worked on fixing them. 



## Next steps

Finish implementation of Binary Trees and move to implementing different balancing trees.



#### Image reference: 

Image presented in this post is taken from Wikipedia and "Selected Design Patterns" lecture slides - [https://slideplayer.com/slide/6641380/](https://slideplayer.com/slide/6641380/?fbclid=IwAR0IfrNj_HEX0g6OdYLi6lymiEnXrUv3m7jXnI-TN13SK_euNhAVxdAhUDg)

