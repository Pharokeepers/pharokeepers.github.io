---
layout: post
author: smi
date: 2019-08-11 08:00:00 +0200
categories: pharo
title: Strategy Design Pattern
comments: true
---

I have already written about the [null object](https://pharokeepers.github.io/pharo/2019/07/28/Null-Object-Pattern.html) and the [state](https://pharokeepers.github.io/pharo/2019/08/02/State-Design-Pattern.html) design patterns and their [use in designing and programming abstract data structures](https://www.cs.rice.edu/~javaplt/papers/sigcse1998.pdf), with an emphasis on binary trees. In this post I decided to write about the [strategy](https://en.wikipedia.org/wiki/Strategy_pattern) design pattern as it is a great way of extended existing trees by adding different balancing strategies.  The strategy pattern is very similar to the state and null object patterns, but they solve different problems. 



## Introduction

The strategy pattern is a behavioral design pattern that allows the program to select an algorithm (from a list of similar and interchangeable algorithms) at runtime. Similar behavior can be achieved by using switch and if control structures, but at a cost of greater complexity.  The key idea is to encapsulate each algorithm in a polymorphic class that extends the (usually implemented as an abstract class or interface) "Strategy", while the "Context" class relies on composition to select and change strategies at runtime. 



![](https://www.tutorialspoint.com/design_pattern/images/strategy_pattern_uml_diagram.jpg)



The [previous image](https://www.tutorialspoint.com/design_pattern/strategy_pattern.htm) demonstrates the use of the strategy design pattern. The interface **Strategy** is implemented by a list of concrete strategies: **OperationAdd**, **OperationSubtract** and **OperationMultiply**. The **Client** program (**StrategyPatternDemo**) sends a request to the **Context** class, which then selects an appropriate strategy. The **Context** class has a reference to a **Strategy** and at runtime selects one concrete strategy from the list, and then executes the algorithm implemented by that concrete strategy.  

The following images, taken from [RefactoringGuru](https://refactoring.guru/design-patterns/strategy) and [SourceMaking](https://sourcemaking.com/design_patterns/strategy), respectively, shows a more illustrative example of the strategy design pattern from real life. 



![](https://refactoring.guru/images/patterns/content/strategy/strategy-comic-1.png)



![](https://sourcemaking.com/files/v2/content/patterns/Strategy_example1-2x.png)



In the previous example we (the client) choose a way to get to the airport based on the budget and time needed. The options are self transport, the bus or the taxi - and each one represents a different concrete strategy. All this different concrete strategies solve the same problem in a different way and with different constraints, and we may choose one of them at "runtime". 



## Advantages and Disadvantages 



#### Advantages:

1. Algorithms are grouped in a class hierarchy and are easily changed, replaced and extended. A new algorithm (with a same interface) can easily be introduced.

2. The application behavior is easily changed at runtime. 

3. The code is cleaner by avoiding unnecessary switch and if control structures that have to check each time what behavior is expected. 

4. The algorithm is decoupled from the main class (context), which makes it perfect for use with tree data structures. 

   

#### Disadvantages: 

1. When designing strategies, extra effort needs to be put in designing the interface and how different strategies are interchanged. The Strategy interface must provide an interface for all required behaviors, while a concrete strategy need not implement all interfaces. 
2. Strategies may require more memory, but this is easily avoided by using a singleton pattern. 
3. Strategies may be slower because of the extra time needed to create a new strategy object, but this can also be avoided by using the singleton pattern. 



## Conclusion 

Strategy pattern is an excellent way to decouple the application architecture from the algorithm it uses. This reduces the complexity and makes the code more readable and maintainable. It allows the class to change its behavior at runtime, and a new behavior can easily be added. It has a few drawbacks, which can be avoided by proper use of the singleton pattern. The strategy pattern is very useful when implementing balancing trees, as the tree data structure remains the same, but the tree can choose different balancing strategies at runtime.  



#### Images

Images are taken from [TutorialsPoint](https://www.tutorialspoint.com/index.htm), [SourceMaking](https://sourcemaking.com/) and [RefactoringGuru](https://refactoring.guru/). All links are provided in-text.

