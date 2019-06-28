---
layout: post
author: nm
title: "Force based layout"
date: 2019-06-28 14:00:00 +0200
categories: jekyll update
comments: true

---

<p>This week I have been working on implementing Force based layouting algorithm. Which was not such an easy task, that I haven't manage to finish completely.</p>
Let's start at the beginning. What is a force based layout (force directed layout)?<br>

>It is a drawing algorithm used to position the vertices (nodes) in a graph by using force system applied between edges and vertices.

![](/images/ForceBasedLayout.png)

<p> Usually, we use spring-like attractive forces to attract pairs of endpoints of edges towards each other, and at the same time, repulsive forces, similar to ones of electrically charged particles, to separate all pairs of nodes.<br>
In a balanced state of this system, the edges tend to have a uniform length (because of spring force) and nodes that are not connected with an edge, tend to be further apart (because of electrical repulsion). </p>

Here is an [interactive force based layout](https://observablehq.com/@d3/force-directed-graph).

Try moving one vertex (by clicking on it and dragging it). How the rest of the group is reacting? <br>
Notice that they are following, but not exactly, even the one we explicitly moved is not staying in the chosen place. So we get a bit different representation, after moving one node. Why is this happening?<br>
Well, because of the forces we are choosing. By changing the position of one node, the force for this node and his edges, change. This change affects the movement of the rest of the nodes.
