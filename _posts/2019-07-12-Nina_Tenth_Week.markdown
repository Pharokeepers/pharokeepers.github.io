---
layout: post
author: nm
title: "Ordering in a line"
date: 2019-07-12 09:38:00 +0200
categories: jekyll update
comments: true

---

<p>This week I have been more oriented towards the Roassal and connecting my layouts to it. With the help of Milton (original Roassal creator) we manage to establish the connection. </p>

![](/images/RoassalGif.gif)

<p>Beside this I continued with refactoring the code, by changing some names and improving the architecture of my classes, giving better descriptions and fixing some small mistakes.</p>

- <https://github.com/medicka/PharoGSoC/commit/1f15b713c08768656b8cb60b0651232419a79537>
- <https://github.com/medicka/PharoGSoC/commit/bd60f274896c88bb3ad91516a834a36ba727a8a1>
- <https://github.com/medicka/PharoGSoC/commit/6a31ea09686448d428aaf53cd52309ffb28c8e0d>
- <https://github.com/medicka/PharoGSoC/commit/f36bf344f93b409319dd90e3c93f58323e7e7b56>
- <https://github.com/medicka/PharoGSoC/commit/484819e425936bbd3378198e1bd4d6efafdd106d>


<p>I also added trait for edges, implementing empty methods in traits (methods that need to be implemented in the classes that use this train) and improve translation. </p>

- <https://github.com/medicka/PharoGSoC/commit/6b079e52633c6ba4504fa0b3aa26485ec9376d77>
- <https://github.com/medicka/PharoGSoC/commit/18ce2bdff0a90b4b43376b9d92005571b5fe2a46>
- <https://github.com/medicka/PharoGSoC/commit/b93847ebd06e101387ab6bf5bf7337088c94507d>

<p>The main focus of this week at the end was adding a new type of layout, line based ones. </p>

- <https://github.com/medicka/PharoGSoC/commit/e01c61dfb55e70445d20bb1feb0ee0b36698f251>
- <https://github.com/medicka/PharoGSoC/commit/52f6f486f4a1b097b628942336ae44c4ac148f7e>
- <https://github.com/medicka/PharoGSoC/commit/f1820c2fd63d24fde1554e440442e803c15aaab6>
- <https://github.com/medicka/PharoGSoC/commit/a5cf329a2f83a4330e94ef72f86142008ccce11a>

<p>In some cases, just seeing our graph in a linear structure is very useful. We can implement properties based on which the size of the vertex is determiened, therefore just looking at them in a vertical or horizontal line can reveal a lot of information. </p>

![](/images/HorizVertic.gif)

