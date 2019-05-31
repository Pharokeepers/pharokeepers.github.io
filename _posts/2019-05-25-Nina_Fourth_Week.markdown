---
layout: post
author: nm
title: "Beginner tips"
date: 2019-05-31 10:38:00 +0200
categories: jekyll update
comments: true

---

As said last week I would like to share some useful hints how to deal with Pharo-Git connection if using Windows. :smile:

Git is a really powerful tool, which is being used regularly, especially if we are working on an open source project. Therefore more programming languages and environments develop a connector, to facilitate using git and GitHub. If we are talking about the Pharos latest version, then that is [Iceberg](https://github.com/pharo-vcs/iceberg).

Iceberg works nicely on Pharo 7.0, but I will not get into its details here. What I want to talk about is some basic tips for beginners, when trying to use GitHub with Pharo. I am separating Windows here, because Pharo is not being mainly developed for this OS, so there are some tricks you need to know:

1. For connecting to git use [SSH key](https://jumpcloud.com/blog/what-are-ssh-keys/). 
![](/images/SSHPharo.png)
2. If you are making your first repository with Pharo, it is a good idea to watch some tutorial, like:
 * https://www.youtube.com/watch?v=PK2yCu2rWCc&feature=share&fbclid=IwAR03niS_4hGtvWYpKhoauj9Qx1gmlmF8L2CD5X2x-158QcfPuCzgJgbLhBo
 * https://www.youtube.com/watch?v=77XrcO4jM8Y&feature=share&fbclid=IwAR2DkmeudfJelMriW7qUPhAhrCVGsJL6dOgl5030jcFul5Y3xEVwfFNEN4U

3. Make your local repository, on a path close to C. Don`t bury it too deep.
4. If a message next to your newly created repository is *not loaded*, don`t worry. Add packages to it and press right click *load*, to continue.

Extra hint: When saving an image it is always a good do it in an automatically created folder. Reason for this is that images should be close to C as well, and that Git can`t read everything. If you save your image in folder with a lot of different type files, that may have numbers in names, you will come to a problem. While trying to upload to repository from that image, you will encounter an error. Git will not be able to go trough the list of these files, to reach your image address. This will automatically stop the process of adding packages to repository.
