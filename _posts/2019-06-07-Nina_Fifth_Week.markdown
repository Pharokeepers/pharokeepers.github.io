---
layout: post
author: nm
title: "Graphs #1"
date: 2019-06-07 10:56:00 +0200
categories: jekyll update
comments: true

---

<p>First couple of weeks I have been focused on Pharo. Its syntax, environment and connections. Which has been very helpful, for the implementation part of my project.</p> 
<p>Now it is time to switch to other big part, and that is Graphs. Since they are central structure on which my whole project stands on, it is important to have a good understanding of them.</p>

Let us begin with some basic questions.
<br>
**What is a graph?**

>Definition: A graph is a set of vertices and a collection of edges that each connect a pair of vertices. [^1]

![](/images/picGraph.png)


Mathematical notation is: 
> G= (V, E) 

Where G is graph,  V is set of vertices (nodes) and E is set of edges.

We recognize three types of Graphs:
1. Undirected (edges have no direction) 

  ![](/images/picUndirected.png )

2. Directed (it matters from which vertex, edge starts; we call these edges arcs)

  ![](/images/picDirected.png)

3. Weighted (each edge has a weight value)

  ![](/images/picWeighted.png)

<br>

**Why graphs?**

There are so many uses for graphs: in mathematics, engineering, programming... To answer this question generally it would be too complex. But why did I choose them is much easier.<br>
One of the uses for graphs is representing a network of roads between cities (each city is a vertex, every road connection is edge). This way we can see who can travel where. As I spend some time in researching code refactoring, I thought it would be interesting to see the program code the same way. Classes as vertices and edges as calls. We can follow dependencies easier. Also see which information can travel where. :smile:
 
<br>
<br>

[^1]: Definition taken from [Algorithms, Fourth edition](http://www.albertstam.com/Algorithms.pdf) by Robert Sedgewick and Kevin Wayne; page 518.
