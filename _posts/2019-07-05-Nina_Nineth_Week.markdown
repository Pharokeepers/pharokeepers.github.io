---
layout: post
author: nm
title: "Integrating with Telescope"
date: 2019-07-05 10:38:00 +0200
categories: jekyll update
comments: true

---

<p> The start of this week was devoted to refactoring.</p>

Updating baseline classes. We changed the implementation in such way that it is easier to import the code to new Pharo image. Changing some class and method names, so that they will be easier to understand. Making a better architecture for tests. Added some abstract classes which were missing, like AbstractEdge. Added some missing test.

- <https://github.com/medicka/PharoGSoC/commit/328663d3255d0e1ef5a9a736e482ff09d4cd11c6>
- <https://github.com/medicka/PharoGSoC/commit/6093cc3e214309d552e94520b6921697c082ca41>
- <https://github.com/medicka/PharoGSoC/commit/1ee4fedbab47069b5e111a710c3a820ac83d05b1>
- <https://github.com/medicka/PharoGSoC/commit/b443375e5c988e525d23ecb5659b6dbf51fe01b7>
- <https://github.com/medicka/PharoGSoC/commit/b3ded010d11f41c548ddba66b0bd97c83f1bf985>

<p> After refactoring I spend some time working with my mentors Cyril and Guillaume on integrating my layouts, with Telescope visualization. It turned out, that the task was not so complicated, so we manage to do it very quickly. </p>

This required some changes in default values for layouts and expected results in connected tests.  

- <https://github.com/medicka/PharoGSoC/commit/b446d93d774b771e8f43d2b5e32ab6c0e5a13ab6>
- <https://github.com/medicka/PharoGSoC/commit/edc92bcc8cd81bb44aacd00e6e8c030da58fbeef>
- <https://github.com/medicka/PharoGSoC/commit/844aa6b52bc585e282f002a94c68003ba8781e95>


<p>In the illustration below I will show what we have done so far.</p>

![](/images/ezgif.com-video-to-gif.gif)

As you can see, with some given graph (in this case it is consistent of 14 nodes and 11 edges) we have a list of possible layouts. First, we see how the cicle layout looks like, and then we switch to the grid.

