---
layout: post
author: smi
date: 2019-05-26 10:00:00 +0200
categories: pharo
title: Pair Programming - Part II 
comments: true
---

Last week I wrote a [post](https://pharokeepers.github.io/pharo/2019/05/19/Smiljana-Week-2-Pair-Programming.html) post about advantages and disadvantages of pair programming. I received some feedback so I decided to do more research, consult the scientific literature and write a follow-up. 

In my last blog post I wrote:

 *Nevertheless, pair programming also has a few drawbacks (compared to individual programming) like increasing the overall project cost and the total number of man-hours (amount of work done by an average programmer in one hour) needed to deliver a finished product .*

I was looking for evidence related to this argument. Most of the results presented here are taken from papers ["Strengthening the Case for Pair Programming", by L. Williams et al](https://dl.acm.org/citation.cfm?id=626149&fbclid=IwAR220NQuFNx3sI3om0zl6Os5Fs-K65Rqfsyvs_qo0lRN_1-3UbOGAYVpsaM). and ["The Costs and Benefits of Pair Programming" by A. Cockburn and L. Williams](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.26.9064).  

What I wrote was one of the biggest misconceptions about pair programming, that this approach will significantly increase the code development expanses. This week I learned that **the overall increase in cost is only about 15%** (and not a 100% as one might think - i.e. two programmers do a job that just one can do), which is easily repaid in higher quality code, fewer errors and a significant reduction in refactoring, bug fixes and testing needed.

Pair programming can also be more enjoyable then working alone and allows for a quicker dissemination of knowledge, good practices and design principles, which is of vital importance for large systems. One way to ensure that knowledge is communicated between coders is to have regular pairings between different team members. 

## Benefits of Pair Programming

In my previous post I only listed some of the advantages of pair programming over individual programming. I would like to give an extended list with more detailed explanations of how pair programming can bring value to the project.

- **Higher quality code**: Pair programming allows a better understanding of the task at hand and can produce a  different perspective and solution to the problem before any code is written. Two programmers can discuss about different solutions and design principles, which can easily be overseen by a single programmer working alone. 
- **Safer code**: Since one programmer is coding while the other programmer is reviewing the code it is much easier to detect errors while they are made. Massive bugs are almost completely avoided. 
- **Overall production time is reduced**:  Early detection of bugs and a higher quality code can reduce the overall time needed to produce a final product (faster time to market). It can also allow for easier maintenance and delivery of new functionality to a longer living system, which will reduce time in the long run. 
- **Improved user experience**: Fewer errors and other issues will improve the user experience and can increase the number of clients, which will increase revenue. 
- **Better and happier programmers:** Pair programming increases communication and provides a better distribution of knowledge about the project, company, workflow and programming in general. This allows for faster training of junior programmers and increases the productivity by minimizing distractions - which contributes to more efficient working hours. Most programmers have reported that they find pair programming fun and enjoyable, and they are generally more satisfied with their job. 

## Conclusion 

What I love about Pharo community is that it's learning oriented. I wrote something that wasn't true, so I got resources to learn from. I learned that pair programming doesn't actually increase the overall project cost in the long run and brings other benefits with it. I had great experience with pair programming the past two weeks  and find it very fun and useful.  I'd definitely  recommend pair programming as a learning method for novices to quickly tackle new problems, it helped me a lot.

