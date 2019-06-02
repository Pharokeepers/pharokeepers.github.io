---
layout: post
author: smi
date: 2019-06-02 08:00:00 +0200
categories: pharo
title: Baseline
comments: true
---



[GSoC 2019](<https://summerofcode.withgoogle.com/>)  [Pharo](<http://pharo.org/>) coding phase has begun! I have started working on the Containers project, polishing the readme files, and adding and fixing class comments and tests.

The main idea behind the Containers project is to collect alternate collection data structures and refactor them in separate packages so that they are modular and can be loaded separately, as well as add some new collections.

Each readme file will contain instructions with code snippets that show how to load the package and its dependencies, e.g:

## Loading

```
Metacello new
   baseline: 'ContainersTrie';
   repository: 'github://Ducasse/Containers-Trie/src';
   load.
```



## If you want to depend on it

```
spec 
   baseline: 'ContainersTrie' 
   with: [ spec repository: 'github://Ducasse/Containers-Trie/src' ].
```



When I first came across this, I wasn't sure what to do with these code snippets and didn't know much about Metacello and baselines. 

During this week I was trying to learn and understand how to use these tools and to test the code snippets before writing my own.

#### Simple trick:

If you want to load the project you can just open a Playground, paste the code snippet under Loading section and execute it and that's it. So simple and easy and you have a project loaded locally on your Pharo image.

#### What about handling dependencies with baselines?

The Pharo [wiki](https://github.com/pharo-open-documentation/pharo-wiki/blob/master/General/Baselines.md) is an excellent resource. Reading Deep into Pharo book, chapter 9: Managing Projects with Metacello gave me a bit clearer picture about what was going on.

Metacello is a package dependency management system. It helps to load packages correctly. Metacello uses baselines to define the basic structure of a project: packages and required projects. Also  baseline defines the order in which packages are to be loaded and from which repositories. 

So if you want to depend on a Container project you need to add the "If you want to depend on it" code snippet to your project's baseline and Metacello will take care of the rest.

You will probably define BaseOfYourProject as a separate package. In it you will have BaseOfYourProject class which will be a subclass of BaselineOf:

```smalltalk
BaselineOf subclass: #BaselineOfYourProject
	instanceVariableNames: ''
	classVariableNames: ''
	package: 'BaselineOfYourProject'
```

And in that class you will need to write a *baseline:* method with dependencies you want:

```smalltalk
baseline: spec
	<baseline>
	spec
		for: #common
		do: [ 
				spec
					baseline: 'ContainersTrie' 
   				    with: [ spec repository: 'github://Ducasse/Containers-Trie/src' ].
	    	 ]
```

This is a very simple example with only one external dependency. You can do a lot more with baselines which is described on the [wiki](https://github.com/pharo-open-documentation/pharo-wiki/blob/master/General/Baselines.md) page.

You have your simple project with one external dependency and now what? Now we need to load it. We can use Playground for this as well.

```smalltalk
Metacello new
	baseline: #YourProject;
	load
```

And that's all the magic :)  

This helped me check if "If you want to depend on it" code snippets are correct and you can actually use them to load external projects.

