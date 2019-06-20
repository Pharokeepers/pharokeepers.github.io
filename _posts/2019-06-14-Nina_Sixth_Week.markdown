---
layout: post
author: nm
title: "Graphs #2"
date: 2019-06-14 11:56:00 +0200
categories: jekyll update
comments: true

---

<p>This was an exciting week. I finished the implementation of my first layout. :tada: :confetti_ball: :tada: :confetti_ball: :smile: </p>
<p>Let us continue with exploring graphs. By now we understand the basics, so we will go a step further.
One of the reasons why, by using graphs we can accomplish so much, is that graphs have a set of algorithms for traversing them, two of which are especially well known, BFS and DFS.</p>
<p>First, we explain what traversing means. <br>
The word definition is: travel across or through. In the context of graphs, traversing means moving through the graph, visiting nodes (vertices) by using the edges.</p>

BFS - breadth first search
> Single-source shortest paths: Given a graph and a source vertex s, support queries of the form *Is there a path from s to a given target vertex v?* If, so find a shortest such path (one with a minimal number of edges). [^1]

This is what we are looking for: the shortest path from source s to given vertex v. The method for solving this is using BFS.

**What does BFS do?**<br>
Let's explain on an example. 

![](/images/Graph.png)

Source vertex is 0, so BFS algorithm, takes this vertex first. Now he visits all his neighbours, that have not been visited before, in our example that would be 1, 3 and 8. When a vertex has no more new neighbours to visit, it is discarded, and the first of his neighbours is taken (in our case that is 1). Now the process repeats. We are visiting all neighbours, by from vertex 1.

So the example continues like this:<br> 
> 0->1, 0->3, 0->8 no more neighbours;<br>
1->7 no more neighbours;<br>
3->2, 3->4 no more neighbours;<br>
8, there are no neighbours, that haven't been visited so far;<br>
7, there are no neighbours, that haven't been visited so far;<br>
2->5, no more neighbours;<br>
4, there are no neighbours, that haven't been visited so far;<br>
5->6, no more neighbours.<br>

With this we have finished our algorithm and visited all vertices.

Now if we choose one vertex for a goal, like 4, we can just follow the path to it, and this will be the shortest one existing.
> Path: 0->3->4 

This kind of algorithm is used by navigation for finding the shortest path from one place to another. <br>
So you can see the amount of problems that are solved easily because of them.
 <br>

 [^1]: Definition taken from [Algorithms, Fourth edition](http://www.albertstam.com/Algorithms.pdf) by Robert Sedgewick and Kevin Wayne; page 538.
