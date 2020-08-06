---
author: jordan-buysse
date: 2020-5-28
layout: post
slug: metaprogramming-ruby
title: "Metaprogramming and Ruby"
categories:
- Research and Development
- Grad Student Research
- Learning Notes
tags: 
- Ruby
- Computer Science
---

At Flatiron, we start out with Ruby. I can’t say I love the language on an aesthetic level (implicit returns and the ‘do’ keyword grate on me for some reason), but it was worth this brief foray into Ruby just to see get some exposure to Ruby’s take on metaprogramming. On a conceptual level, metaprogramming refers to processes where languages can read, generate, or modify pieces of themselves. I’m not going to delve into the theoretical stuff here, though. In practice I’ve found this often means blurring the distinction between compilation and runtime, a practice that in its most radical form via Lisp--as Paul Graham says “the whole language is always available”--including all the intermediary bits of in-between computer speak.[^1] What this all means for Ruby, in my experience so far, is two things. 

## Monkey-patching

The first is ‘monkey-patching’--the ability to amend methods in Ruby’s default classes on the fly. For example, maybe you’re on island time. You could dig in to Ruby’s default classes and change the definition of the weekend:

	module CoreExtensions
  	 module DateTime
    	  module BusinessDays
      	   def weekday?
            !sunday? && !saturday? && !friday?
      	   end
    	 end
  	end
	end

[Thanks to Justin Weiss](https://www.justinweiss.com/articles/3-ways-to-monkey-patch-without-making-a-mess/) for the example. There’s not much benefit to doing this via monkey patching, of course, and it’s certainly not how I’d solve the problem in the wild. But this example goes to show how you can build robust packages for Ruby based on modifying core ‘upstream’ classes in the Ruby default library. “Awesome Print” was a popular one for our Mod 1 projects, which runs via modifications of Ruby’s default IRB (aka “interactive Ruby” aka REPL aka Ruby’s read-eval-print loop). “Awesome Print” brings Ruby’s “Pretty Print” to life via full colors and new features. But as the docs say, Awesome Print really is just “exposing their internal structure with proper indentation,” building alongside rather than on top of Ruby’s existing methods.
## Metaprogramming to define new classes and methods
The other example I want to talk about very briefly is ActiveRecord, a source of a lot of the ‘magic’ people talk about when they talk about Rails and which, I’d argue, is the key piece of tech that allows the Flatiron curriculum to jump from CLIs to non-templated full-stack web apps so quickly. [^2] There’s way to much to cover on the topic of AR and metaprogramming so I’ll just note one simple example: Active Record’s “Dynamic Finders,” which make ugly database queries into friendly (yes, ‘magic’, feeling) natural language queries. If you have a field for spirit_animal on your User model for example, AR will generate a method called find_by_spirit_animal for free. find_by_ functions are simple plug-and-play templates that insert the field name into a method with everything else defined.
Metaprogramming! It’s everywhere. Especially in the ‘magic’ parts of Rails magic. I wrote this blog mostly to try and take a nebulous, theoretical concept, and pin it down to a couple of things I’ve done in Ruby. Hope you can find some use for it.

## Endnotes
[^1]: As a side note, Lisp was the first programming language I ever had someone actually try to teach me, circa 2003, when I was in middle school. I was at a computer camp of some sort---maybe the actual curriculum was learning to build websites in Dreamweaver, or make flash animations, or something? All I really remember was two things. The first was really only wanting to play Age of Empires, which was installed on all the computers. The second was that one of the instructors there taught a mini class on Lisp programming. I remember reading the Lisp docs for some reason, not understanding a thing, especially a cryptic mention of illegal lambda functions, whatever that meant.
[^2]: From what I understand, other campuses take a lengthier route through Sinatra other Rack related things first