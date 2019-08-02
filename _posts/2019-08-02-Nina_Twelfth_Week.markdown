---
layout: post
author: nm
title: "Trees"
date: 2019-08-02 09:35:00 +0200
categories: jekyll update
comments: true

---

There have been some interesting changes in the last two weeks. The first of which is that I decided to change the name of my project ( repository ) to *graPharo*.<br>
Next, I have been working on optimizing some layout algorithms. Equidistant circle and weighted circle have been implemented in many other projects, but the algorithms that were used, have not been working properly in every situation. <br>
If we are talking about equidistant circle, the problem was found when we change the shape of vertices to rectangles or if vertices have different sizes. Than the positioning would not match the definition of equidistant ( to put all vertices on the circle in such a way, that they are equally distant from their neighbours).
In the original algorithm to calculate angle of separation and the gap, we used only each vertices height, which worked well if the width is absolutly the same. But since that is not the case, we had to find the way to recognize which dimension is needed from which vertex and then use that one in the calculation. <br>
Similar problem was with weighted circle, to calculate the weight factor of a vertex, we would only use height. Which would make a mistake if the width of the vertex is bigger than the height. For this reason, in the optimized version, we choose bigger of two dimensions and use it to make the calculation.

- <https://github.com/medicka/graPharo/commit/6d69790d3f031775f667f9e6954e511e6221b48a>

![](/images/Circles.gif)

I also implemented new layout: tree layout. This positioning algorithm is putting vertices in a tree structure. Every tree has a root. in our algorithm we chose that all the vertices with no parent should be root nodes (no in neighbours). One new thing that I decided to add to tree algorithm is orientation. Now the layout allows you to give him, which orientation you want to see. There are four of them and they are shown on the picture below.

![](/images/TreeLayout.png)

- <https://github.com/medicka/graPharo/commit/ca529f539f484cd05fd67230426cfe5461bedad2>

In the past two weeks I have been doing a lot of refactoring, adopting better architecture adding new ways of translation and adding more tests.

- <https://github.com/medicka/graPharo/commit/c2684a87c8de11d5bc8ee984a31e61b91fddc042>
- <https://github.com/medicka/graPharo/commit/9e39810ff6715d4bf1217e1f8c204749f53ff725>
- <https://github.com/medicka/graPharo/commit/4aa4a7039dce917a9d45e53d3898784603461b3b>
- <https://github.com/medicka/graPharo/commit/68c3dfbdb03e69273d9a00d6181e6d94d33d1a7d>
- <https://github.com/medicka/graPharo/commit/68ad1fabdd97138c6f46e9bb0cd1906aa8ab24aa>
- <https://github.com/medicka/graPharo/commit/18e612e359b9b95346372b26ee871d9836f142e8>
