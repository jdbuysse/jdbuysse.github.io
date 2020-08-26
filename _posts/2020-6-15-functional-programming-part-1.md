---
author: jordan-buysse
date: 2020-6-15
layout: post
slug: fp-part-1
title: "Functional Programming with Dr. Frisby, Part 1: Introduction and First Class Functions"
categories:
- Research and Development
- Learning Notes
tags: 
- Javascript
- Computer Science
- Functional Programming
---

By default, I’d say my brain is much more comfortable with object oriented programming. I have lots of cool friends hip to the latest and greatest in the dev world, and I get the sense over and over again that the functional club is a cool place to be. But I’m the first to admit--so far, I don’t really get the appeal. This post is the first in a potential series where I try my damndest to get my brain around functional paradigms and what appeals to people so much about the whole thing.[^1] Since I see lots of Javascript in my future, and frankly I’m not that interested in writing object-oriented Javascript, this is the next logical step.
I’ll be tackling the functional landscape through an open access book, Professor Frisby’s Mostly Adequate Guide to Functional Programming, since I’ve had it recommended to me, and it comes with exercises. I had cracked this book open before I had the general grasp of Javascript I have now, but it’s time to revisit now that I’ve more than dipped my toes into that world and have done some functional programming myself over the last six months. So if all goes to plan I’m going to blog my experiences working through the examples and conceptual stuff in the textbook. Let’s get started.

## Think Mathy

I might have already figured out part of my aversion to functional programming. Professor Frisby’s first example involves him walking through an ugly class-based snippet: 

	class Flock {
  	 constructor(n) {
    	  this.seagulls = n;
  	}
	
	conjoin(other) {
    	 this.seagulls += other.seagulls;
    	 return this;
  	}
	
	breed(other) {
    	 this.seagulls = this.seagulls * other.seagulls;
    	 return this;
  	}
	
	const flockA = new Flock(4);
	const flockB = new Flock(2);
	const flockC = new Flock(0);
	const result = flockA
	
	.conjoin(flockC)
	.breed(flockB)
	.conjoin(flockA.breed(flockB))
	.seagulls;
	// 32

and reducing it down to mathematical properties:

	// associative
	add(add(x, y), z) === add(x, add(y, z));

	// commutative
	add(x, y) === add(y, x);

	// identity
	add(x, 0) === x;

	// distributive
	multiply(x, add(y,z)) === add(multiply(x, y), multiply(x, z));

Now, if I’m a bit nervous on math, I am pretty cool with deductive logic (shout out to [Warren Goldfarb](https://www.hackettpublishing.com/deductive-logic), and Eddie Cushman’s Logic 101 class in college) which was the only math-adjacent class I’ve ever really grokked. Up with deductive logic! I’m feeling more comfortable already.

## Why writing first class functions matters

  I have to be much more disciplined about how I write first class functions.

  1. More code to change. if you allow for an arbitrary number of arguments, you don’t need to go back and specify every time something changes.
  2. Names! Your code gets crowded and avoiding naming intermediary variables saves you a bunch of headaches.
  3. First-class functions naturally result in more re-usability and allows for DRYer code

Dr. Frisby even gives us some choice snippets from real software published on NPM that fails to adhere to good first class function practice. Suffice it to say that, for now at least, I'm warming up to the idea.

## Endnotes
[^1]: I actually set out recently to understand more about OO javascript and that language’s [particular form of inheritance](https://davidwalsh.name/javascript-objects), *but it was a lot to deal with*. Stay tuned for a post on that.
