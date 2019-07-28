---
layout: post
author: smi
date: 2019-07-28 10:00:00 +0200
categories: pharo
title: Null Object Pattern
comments: true
---

A [null object](https://en.wikipedia.org/wiki/Null_object_pattern) is an object with a defined neutral behavior, which allows us to write a cleaner and faster code. It can be said that a null object "[reflects a do nothing relationship](https://www.tutorialspoint.com/design_pattern/null_object_pattern)". 

## Null Object Design

When working with references, one is usually forced to check if that reference exists (i.e. is null) before invoking any method. Instead of putting a lot of if-null checks which reduce readability, one can use a null node design pattern to provide a polymorphic object with a "default behavior" when no data is present. 

Following image ([taken from GeeksForGeeks](https://www.geeksforgeeks.org/null-object-design-pattern/)) shows a simple null object design. 

![](https://contribute.geeksforgeeks.org/wp-content/uploads/NullObject.png)

In the previous image the **DependencyBase** represents an abstract base class that describes the interface that some **Clinet** may use. **Dependency** implements all abstract methods as expected, while the **NullObject** implements a default (do nothing/return 0/return empty collection) behavior of all methods listed by the **DependencyBase**, and as such can also be used by the **Client**.

The [following image](https://www.tutorialspoint.com/design_pattern/null_object_pattern) shows a simple example of a null object design pattern combined with a factory (factory design pattern) which decides whether to create a real object or a null object.

 ![](https://www.tutorialspoint.com/design_pattern/images/null_pattern_uml_diagram.jpg)

## Advantages and disadvantages

Advantages:

1. There is a class hierarchy, so a null objects can be used instead of real objects. 
2. Makes the Client code a lot cleaner and simpler, the client no longer has to worry about getting a null reference. It will always get a reference to a valid object, even if that object does nothing. 
3. It can also speed up the code, by eliminating unnecessary if checks. 

Disadvantages:

1. Can waste memory if there are a lot of null objects. To solve this, one usually implements the null object as a singleton. 
2. The "do-nothing" behavior may not be well defined. If there are multiple clients, they must all "agree" on what a default behavior is, or we may need to implement different null objects.
3. Sometimes a null object must be replaced by a real object. This can be implemented by using the state design pattern - which will be described in more detail in a future blog post. 

## Conclusion

As we have seen, the null objects may have some disadvantages which can be avoided by making a smarter design. Null node can reduce the complexity of the Client code which make this extra time to make a better design worth it. We are using the Null Object design pattern (combined with a state pattern) for implementing the tree data structure. 



#### Image references

All images are taken from Geeks-For-Geeks and the TutorialsPoint websites. All references are provided in-text. 