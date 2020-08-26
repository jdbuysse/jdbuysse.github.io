---
author: jordan-buysse
date: 2020-7-02
layout: post
slug: fp-part-2
title: "Functional Programming with Dr. Frisby, Part 2: Purity & Currying"
categories:
- Research and Development
- Learning Notes
tags: 
- Javascript
- Computer Science
- Functional Programming
---

> *This post is part of a series on functional programming. [You can check out part 1 here](http://jordanbuysse.com/fp-part-2.html)*

In the last post, I wrote about “first class functions” in a Javascript--a key paradigm for the language that often (and I’m very guilty of this) gets ignored in the process of writing code. Functional programming at its core is about simplifying code and making it easier to maintain. This is clear enough in the case of first class functions, and Dr. Frisby takes this a step further by introducing the idea of pure functions. The definition is as follows:
>A pure function is a function that, given the same input, will always return the same output and does not have any observable side effect.
In functional programming, we try our best not to *mutate* state: that is, avoid sending in and getting back different forms of the same object. The difference is easily illustrated in the two similar methods slice() and splice(), which return the same thing on a given array once, but only slice keeps the original array intact while splice() chops off a few elements every time. All this purity talk is in the service of limiting *side effects*. It’s not about completely removing them, but limiting the exponential spread of state-dependent idiosyncrasies in order to save ourselves headaches down the road.[^1]

## OK, but why?
Being the OOP person that I am, I can think of a few arguments against this method. The most important to me is the possibility of doing test-driven-development, which I quite like. There’s not so many headaches about state, in theory, if you can effectively model it in your testing processes. But functional programming is about more than just managing state. The real benefits are as follows.
#### Caching
Pure functions are extremely cacheable, speeding up many types of queries and calculations. Usually this is done through memoization (remember reduce()?).
#### Portable / Self-documenting
This one is pretty useful when it comes to web applications. Pure functions both have more documentation about what they do and can be moved around more freely between different service workers, over a socket, or in different database configurations. A lot less stuff to carry around (via copy and paste and installing the same dependencies) from application to application.
#### Testing
Less mocking up of different states in your tests--you can even rely on procedurally generated data to bombard your functions with different inputs in order to do some automated testing.
#### Referential transparency
I’ve already talked about this a bit, but it ties back to the example in part one using ‘equasional reasoning’ aka deductive logic to simplify the seagull program. 
#### Parallelism
In the same vein as functional programming’s _portability_, the separation of state from function allows you to more easily implement parallel processes. No race conditions!
## Currying
OK I have to admit, currying is taking me a bit of time to really wrap my head around. I started with closure, which I sorta understood from seeing some ‘trick question’ type examples, but had to get more familiar with. I remember it now by remembering to ask ‘what does closure enclose?’: the function and the lexical environment in which the function was declared. In a sense, it’s about encapsulating state in functions.
As for currying itself, well, I don’t really have a neat definition formulated for you. If you’re like me, the following example will help clarify (eventually, after a lot of staring):

    const add = x => y => x + y;
    const increment = add(1);
    const addTen = add(10);
    increment(2); // 3
    addTen(2); // 12

The idea of giving the initial ‘add’ function less arguments than it expects is called *partial application*. The goal? To reduce code.

## OK but why?
Here’s a neat trick that helped me see why I’d want to use this in the first place. Consider the following:

    const getChildren = x => x.childNodes;
    const allTheChildren = map(getChildren);

You can move seamlessly between a function that works on a single element to one that can generate an array.

## Endnotes
[^1]: Looking ahead, this is the whole *thing* with hooks versus class-based components in React, in a nutshell.
