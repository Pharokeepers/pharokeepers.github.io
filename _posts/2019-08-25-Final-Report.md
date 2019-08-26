---
layout: post
author: smi
date: 2019-08-25 10:00:00 +0200
categories: pharo
title: Final Report
comments: true
---

Hello everyone. The last three months passed by really quickly and the **Google Summer of Code** (GSoC) **2019** is coming to an end. In this blog post (which is also a part of my final report) I will summarize the main results of my GSoC 2019 project  titled [**New Collections for Pharo**](https://pharokeepers.github.io/pharo/2019/05/12/intro-to-gsoc.html), my overall experience and what I have learned. I am really happy that I had a chance to participate in this GSoC and I can say that this was an incredible experience. 



## Introduction

As many of you already know, [Pharo](https://pharo.org/) is an actively developed, elegant pure object-oriented programming language that comes with an immersive IDE that simplifies testing and debugging and can significantly reduce development time. Pharo also comes with a large set of [existing collections](http://pharo.gforge.inria.fr/PBE1/PBE1ch10.html) (see following figure). There is an existing effort - [The Containers modular library](http://smalltalkhub.com/#!/~StephaneDucasse/Containers), to include many more new collections in Pharo.  This project has attracted the attention of the Pharo community and I had a chance to work on it during this GSoC. 

 ![](http://pharo.gforge.inria.fr/PBE1/Collections/figures/CollectionHierarchy.png){:height="30%" width="30%"}



### Goals

My project goal was to collect, clean test and document alternate collections as well as implement a few new ones (with appropriate tests and documentations) and include them in the library. 

Trees are very important and useful data structures. They have many applications, ranging from computer science and language processing to 2D/3D image processing and rendering, and many more... After a consultation with my mentors and the Pharo community it was decided that I am to implement different Tree collections that can easily be extended and used by other users. 



### End Results

During this GSoC I worked on improving several different containers (e.g. Containers-Stack, Containers-Queue, Containers-Trie, Containers-OrderedMultiMap, and many others). I've fixed mistakes, cleaned and refactored the code, and included necessary documentation and tests. As part of the Containers-Tree library, I added new collections: Binary Trees, N-ary Trees, Binary Search Trees and AVL Trees. Detailed documentation and tests are provided for each new collection. All these collections follow the object-oriented paradigm and are designed  to be easily extended and used by other users. In the next section I will describe all contributions in greater detail. 



## What has been done

Containers library is designed to be modular and as such each collection is independent of the others. During this GSoC I've worked on several different Containers. 

### Contribution Lists

The following list shows GitHub pull requests, each one containing several commits. Ticked boxes indicate that all the changes are merged into the base branch. Most of the commits have been included into the base branch, while a few still await to be merged.  Changes made to the Containers-Tree project are more significant, and they are presented in a separate list. 

- [x] [Containers-SkipList: fix how to depend on it](https://github.com/Ducasse/Containers-SkipList/pull/2)
- [x] [Containers-UniqueOrdered: add how to load and depend on](https://github.com/Ducasse/Containers-UniqueOrdered/pull/1)
- [x] [Containers-Grid: add how to depend on code](https://github.com/Ducasse/Containers-Grid/pull/2)
- [x] [Containers-Array2D: add how to depend on code](https://github.com/Ducasse/Containers-Array2D/pull/4)
- [x] [Containers-OrderPrservingDictionary: remove deprecated method](https://github.com/Ducasse/Containers-OrderPreservingDictionary/pull/3)
- [x] [Containers-PropertyEnvironment: change coverage status button url](https://github.com/Ducasse/Containers-PropertyEnvironment/pull/3)
- [x] [Containers-Stack: edit method comments](https://github.com/Ducasse/Containers-Stack/pull/4)
- [x] [Containers-Array2D: Patch/separate tests](https://github.com/Ducasse/Containers-Array2D/pull/7) 
- [ ] [Containers-Queue: separate tests, add missing tests and comments](https://github.com/Ducasse/Containers-Queue/pull/5)
- [ ] [Containers-Trie: add example](https://github.com/SmiljanaKnezev/Containers-Trie/pull/1)
- [ ] [Containers-Array2D: change coveralls url to Array2D instead of Grid](https://github.com/Ducasse/Containers-Array2D/pull/6)
- [ ] [Containers-OrderPreservingDictionary: Add class and package comments with examples](https://github.com/Ducasse/Containers-OrderPreservingDictionary/pull/2)
- [ ] [Containers-OrderedMultiMap: move tests to separate package](https://github.com/Ducasse/Containers-OrderedMultiMap/pull/5)



Containers-Tree contributions:

- [x] [Publish all the alternate package into Container-Tree](https://github.com/Ducasse/Containers-Tree/pull/4)
- [x] [Add binary node and tree class with getters, setters and other methods](https://github.com/Ducasse/Containers-Tree/pull/5)
- [x] [Fixed an issue - isEmpty](https://github.com/Ducasse/Containers-Tree/pull/6)  
- [x] [Fixed and restructured Binary Tree](https://github.com/Ducasse/Containers-Tree/pull/7)
- [x] [Add a new composite binary tree implementation](https://github.com/Ducasse/Containers-Tree/pull/8)
- [x] [Binary Search Trees (using composite design)](https://github.com/Ducasse/Containers-Tree/pull/9)
- [x] [Add N-ary trees with tests](https://github.com/Ducasse/Containers-Tree/pull/12)
- [x] [Add traversing methods and operations methods with tests](https://github.com/Ducasse/Containers-Tree/pull/10)
- [x] [Fix or operator, and change argument names in AbstractTree](https://github.com/Ducasse/Containers-Tree/pull/11)
- [x] [Add class and method comments for search tree](https://github.com/Ducasse/Containers-Tree/pull/14)
- [ ] [Add class and method comments for n-ary tree](https://github.com/Ducasse/Containers-Tree/pull/13)
- [ ] [Add avl tree with tests and commetns, modify binary search tree](https://github.com/Ducasse/Containers-Tree/pull/15)



### Challenges Faced and Lessons Learned

One of the biggest challenges was designing a tree data structure that can easily be extended and reused for different applications. I started with implementing a [rooted binary tree (and binary search tree)](https://github.com/Ducasse/Containers-Tree/tree/78718336f3236a862bea5fd534e194df61d9a954/src/Containers-BinarySearchTree), for detailed description see [this blog post](https://pharokeepers.github.io/pharo/2019/07/07/SmiljanaBinarySearchTreeinPharo.html). After consulting with my mentors, we decided to *do the things the Pharo way* - i.e. redesign the trees using object oriented approach and design patterns and going from rooted representation to a composite one. This was a demanding task as I had a lot to learn. 

Composite design pattern lets you treat a group of objects the same way as you would a single instance. In our case we can treat a node of a tree the same way as a subtree and consequently as an entire tree. This would let users (clients) treat nodes and compositions of nodes uniformly. 

In our case, with a tree, there was no need to separate node class and a tree class. A tree could be represented as a single node and all the operations that can be performed on a tree you should be able to do on a single node and vice a versa. As a result a tree could be represented with one class. For more details see [this blog post about restructuring trees](https://pharokeepers.github.io/pharo/2019/07/14/SmiljanaBinaryTree.html).

In order to further improve the design and avoid unnecessary *if-checks* I implemented the Null object design pattern. This simplified the code significantly and made it more readable. For a detailed description about the Null Object see [this blog post](https://pharokeepers.github.io/pharo/2019/07/28/Null-Object-Pattern.html).



#### I summarize some key things that I've learned:

- [x] I am more comfortable thinking about object oriented design - i.e *the Pharo way*.
- [x] I realize the importance and advantages of design patterns.
- [x] I learned some new design patterns that I didn't know before.
- [x] I believe I am able to recognize when to use some design patterns and when not to. 
- [x] I feel a lot more comfortable programming in Pharo.
- [x] I learned how to write better tests.

### Code Base

As the **Containers Library** is a big project that is actively being developed, I provide links to the current state of the code at the end of the GSoC 2019. A few commit merges are still pending. For links to the active projects, please see [Active Project Links](#Active Project Links) in the [Auxiliary Links](#Auxiliary Links) section.

- [Containers-Tree](https://github.com/Ducasse/Containers-Tree/tree/78718336f3236a862bea5fd534e194df61d9a954) 

  ---

- [Containers-Trie](https://github.com/Ducasse/Containers-Trie/tree/4d4e8b9973ba9b677d418a5f7746a23d5db54222)
- [Containers-Grid](https://github.com/Ducasse/Containers-Grid/tree/35f048697f027faf1cd0b98c89dd2043b91a64ef)
- [Containers-Stack](https://github.com/Ducasse/Containers-Stack/tree/94911cb597dcef288a82d24cbdbcc95539e66df3)
- [Containers-Queue](https://github.com/Ducasse/Containers-Queue/tree/7124d6441ce7f7444320db46ccbde4dcc3e488eb)
- [Containers-SkipList](https://github.com/Ducasse/Containers-SkipList/tree/f1ce2fc5f0f25f667b3d1993a4ceeeff1f69f41e)
- [Containers-Array2D](https://github.com/Ducasse/Containers-Array2D/tree/cf92fb7ae95da2949dd562b3dfa335f507ea5d08)
- [Containers-UniqueOrdered](https://github.com/Ducasse/Containers-UniqueOrdered/tree/b717cd2f359ef267e8fc221a55c5b6236ad53560)
- [Containers-OrderedMultiMap](https://github.com/Ducasse/Containers-OrderedMultiMap/tree/33e0f1b75e659e110b40afe3fa623c4b0534746a)
- [Containers-PropertyEnvironment](https://github.com/Ducasse/Containers-PropertyEnvironment/tree/867dbd3dcde9425c04234c89918a3ebc6955dc84)
- [Containers-OrderPreservingDictionary](https://github.com/Ducasse/Containers-OrderPreservingDictionary/tree/4dc97329856997cb93fa7af9f4abc05bab232542)



## Overall Experience 

I had a lot of fun during this GSoC but I have also learned a lot. The Pharo community is great and people are always eager to help. I am really happy I had a chance to be part of this community and I hope to continue my work on the Containers library. I can say that this was a very valuable experience.

I would like to sincerely thank my mentors - Stéphane Ducasse, Gordana Rakić, Guille Polito and Yurko Tymchuk for their help and support during this project.



## Plans after GSoC 2019

Containers library is a big project that will be actively developed and maintained well after this GSoC has ended. I plan on continuing to contribute to the Containers library and other Pharo projects, and hope to be an active member of the open source community. 



## Auxiliary Links

### Active Project Links

During the GSoC 2019 I contributed to following projects:

- [Containers-Trie](https://github.com/Ducasse/Containers-Trie)
- [Containers-Grid](https://github.com/Ducasse/Containers-Grid)
- [Containers-Stack](https://github.com/Ducasse/Containers-Stack)
- [Containers-Queue](https://github.com/Ducasse/Containers-Queue)
- [Containers-SkipList](https://github.com/Ducasse/Containers-SkipList)
- [Containers-Array2D](https://github.com/Ducasse/Containers-Array2D)
- [Containers-UniqueOrdered](https://github.com/Ducasse/Containers-UniqueOrdered)
- [Containers-OrderedMultiMap](https://github.com/Ducasse/Containers-OrderedMultiMap)
- [Containers-PropertyEnvironment](https://github.com/Ducasse/Containers-PropertyEnvironment)
- [Containers-OrderPreservingDictionary](https://github.com/Ducasse/Containers-OrderPreservingDictionary)

Biggest contribution was done to the project:

- [Containers-Tree](https://github.com/Ducasse/Containers-Tree)

### Blog

During the GSoC I wrote weekly blog posts about the things I learned and what I did. I include here a list of all the previous blog posts:

1. [New Collections for Pharo](https://pharokeepers.github.io/pharo/2019/05/12/intro-to-gsoc.html)
2. [Pair Programming](https://pharokeepers.github.io/pharo/2019/05/19/Smiljana-Week-2-Pair-Programming.html)
3. [Pair Programming - Part II](https://pharokeepers.github.io/pharo/2019/05/26/Smiljana-Week3-PairProg2.html)
4. [Baseline](https://pharokeepers.github.io/pharo/2019/06/02/BaselineBlogPost.html)
5. [Comparing Ordered Dictionaries](https://pharokeepers.github.io/pharo/2019/06/09/Smiljana-Comparing-Odered-Dictionaries.html)
6. [Prelude to Trees](https://pharokeepers.github.io/pharo/2019/06/15/SmiljanaRootedTrees.html)
7. [Left Child, Right Sibling](https://pharokeepers.github.io/pharo/2019/06/23/Left-Child-Right-Sibling.html)
8. [Tree Application Programming Interface (API)](https://pharokeepers.github.io/pharo/2019/06/30/Application-Programming-Interface-API.html)
9. [Binary Search Tree in Pharo](https://pharokeepers.github.io/pharo/2019/07/07/SmiljanaBinarySearchTreeinPharo.html)
10. [Restructuring Trees](https://pharokeepers.github.io/pharo/2019/07/14/SmiljanaBinaryTree.html)
11. [Self-Balancing Trees](https://pharokeepers.github.io/pharo/2019/07/20/Self-Balancing-Trees.html)
12. [Null Object Pattern](https://pharokeepers.github.io/pharo/2019/07/28/Null-Object-Pattern.html)
13. [State Design Pattern](https://pharokeepers.github.io/pharo/2019/08/02/State-Design-Pattern.html)
14. [Strategy Design Pattern](https://pharokeepers.github.io/pharo/2019/08/11/Strategy-Design-Pattern.html)
15. [M-ary trees](https://pharokeepers.github.io/pharo/2019/08/19/M-ary-trees.html)

### Personal Links

* GitHub: https://github.com/SmiljanaKnezev
* Twitter: https://twitter.com/KnezevSmiljana

