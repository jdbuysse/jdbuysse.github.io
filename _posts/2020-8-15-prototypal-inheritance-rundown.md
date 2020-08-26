---
author: jordan-buysse
date: 2020-8-15
layout: post
slug: protoypal-inheritance-rundown
title: "Prototypal Inheritance Rundown"
categories:
- Research and Development
- Learning Notes
tags: 
- Javascript
- Computer Science
- OOP
---

## Prototypal inheritance
Let’s set the stage here, real quickly: in Javascript, prototypes are not classes. To make a finer-grained point of it, prototypes don’t work based on inheritance (as you might assume if you’re thinking in classes) but rather via delegation. What’s the difference? I quite like the Happy Meal analogy via [Angus Croll](https://javascriptweblog.wordpress.com/2010/12/22/delegation-vs-inheritance-in-javascript/):
>Using inheritance as a vehicle for code reuse is a bit like ordering a happy meal because you wanted the plastic toy. Sure a circle is a shape and a dog is a mammal – but once we get past those textbook examples most of our hierarchies get arbitrary and tenuous – built for manipulating behaviour even as we pretend we are representing reality. Successive descendants are saddled with an ever increasing number of unexpected or irrelevant behaviours for the sake of re-using a few. 
>Delegation is a technique that promotes code reuse by allowing runtime function invocation in the context of a specific instance – regardless of the hierarchical lineage of instance and function.
If you read my [read-along blog posts](http://) about functional programming in Javascript, you’ll notice a similar motif here even in a OOP concept like delegation: don’t make state more complicated than it needs to be! It’s code re-use without the baggage of state. JavaScript does indeed have classes, but JavaScript classes really just syntatic shorthand for inheritance between objects.

## Implementation via __proto__
In Javascript, all  objects have a built-in __proto__ property, which is a reference to another object AKA that object’s ‘prototype’. When you call a property on an object and it’s not in that object itself, Javascript will elevate the call up the chain to look at the next object:

![Prototypal inheritance](/static/img/prototypal-inheritance.jpg)

Every object in JavaScript has a private __proto__ property that links upwards to its prototype, all the way up a chain, through the built in Object (the Platonic idea of an Object, if you will), and then onto null.

## In the wild
You can see prototypal inheritance in action during web development via Javascript's URL API. When you want to grab search params in a URL, you create a new object out of  the URLSearchParams() constructor, which is a prototype that defines utility methods to work with the query string of a URL. 
One last thing I'd like to note, in reference to my [blog post on Ruby and metaprogramming](https://jordanbuysse.com/metaprogramming-ruby.html). In JavaScript, you really don't want to do any monkey-patching. Because of the way JavaScript closure works and the method in which JavaScript is compiled, you don't really want to mess around with monkey-patching in the way you might with Ruby. Doing so would lead to memory inefficiency problems related to how JavaScript reads the protoype chain to optimize code.

## Conclusion

Prototypal inheritance matters, and the importance is easy to overlook by too hastily equating classes from other languages with how JavaScript objects work. Abandoning the constructor pattern of prototypal inheritance in favor of the prototypal pattern of prototypal inheritance is a key mental move when digging deeper into Javascript.
Writing code using the prototypal pattern instead of the constructor pattern will cut off a lot of issues at the pass and lead to more idomatic JavaScript.