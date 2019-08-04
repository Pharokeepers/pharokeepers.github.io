---
layout: post
author: smi
date: 2019-08-02 08:00:00 +0200
categories: pharo
title: State Design Pattern
comments: true
---

This week I continued with implementing different Tree data structures in Pharo, and have investigated the [**state design pattern**](https://en.wikipedia.org/wiki/State_pattern) as a good way of having a single class that can act as both an empty tree and a normal tree. In this blog post I will briefly describe the State Design Pattern and its applications. The state pattern is very closely related to the [strategy](https://en.wikipedia.org/wiki/Strategy_pattern) and [bridge](https://en.wikipedia.org/wiki/Bridge_pattern) design patterns. The **Null object pattern** that I described in [a previous blog post](https://pharokeepers.github.io/pharo/2019/07/28/Null-Object-Pattern.html) can be regarded as a special case of the state pattern. 

## Introduction

[State design pattern](https://www.geeksforgeeks.org/state-design-pattern/) is one of the behavioral design patterns where a class object has an internal state, and based on this state the object can change its behavior  i.e. act as an object of some other class.  [Next figure](https://en.wikipedia.org/wiki/State_pattern) shows a general structure of the state design pattern. 



![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/State_Design_Pattern_UML_Class_Diagram.svg/940px-State_Design_Pattern_UML_Class_Diagram.svg.png)



In the previous picture, **Context** represents the interface which is provided to the client of the program. **Context** refers to the **State** interface for performing state-specific operations (e.g. handle()). **State** defines the interface, which **ConcreteStateA** and **ConcreteStateB** implement. 

**ConcreteStateA** and **ConcreteStateB** represent different states and their *handle()* method defines a different behavior. 

The [following image](https://sourcemaking.com/design_patterns/state), taken from the [Source Making website](https://sourcemaking.com), nicely illustrates the state design pattern. 

![](https://sourcemaking.com/files/v2/content/patterns/State_example1-2x.png)

In this example the vending machine has two states and when money is deposited (**VendingDepositeState**), it will change its state and return the bought item (**VendingStockState**). 



## Advantages and disadvantages 

**Advantages: **

- Easily implement polymorphic behavior. 
- Behavior is determined at run time, and can easily change. 
- It can easily be extended, i.e. new behavior can easily be added. 

**Disadvantages:**

- If there are multiple states, we need a class for each state and the overall program can easily become too complex. But this also provides a separation of concern so it is also an advantage.

- The memory use can be too high, if there are many objects, each one with its own state. This can easily be avoided by making the states singleton objects.

  

## Conclusion 

State design pattern is an excellent way to avoid unnecessary if-checks and move the state-specific block into its own class and use polymorphism. The behavior of the object can easily be changed by providing a reference to a new state, and an existing code can easily be extended to provided different behaviors. The only drawback is higher memory requirements which can easily be eliminated by using other design patterns - i.e. the [Singleton pattern](https://en.wikipedia.org/wiki/Singleton_pattern).



##### Images

Images are taken from Wikipedia and Source Making. Link is provided in-text.