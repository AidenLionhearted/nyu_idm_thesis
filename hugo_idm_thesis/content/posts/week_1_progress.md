---
title: "Week 1 Progress"
date: 2026-09-03T21:06:48-04:00
draft: false
description: ""
tags: []
categories: []

toc:
  enabled: true
  ordered: false
  startLevel: 1
  endLevel: 3
---
# 9/3/2026
## Journal Creation
I decided to go with Github Pages as my journaling platform.  I did this because I want to store all my files in a GitHub repository.  This will make it easy to work on my project from any of my machines.

I chose [Hugo](https://gohugo.io/) as my backend.  It supports markdown format which I am familiar with and can use already built themes.  I chose [rewired](https://github.com/RigleGit/rewired) as my theme.  I liked it because it looked like a command line interface which reminds me of text based games.

I was looking into software that would add the ability to annotate posts to my journal.  I was tinkering with the idea of putting my documents on my Github Pages site.  But this didn't work.  I'm guessing this is because I'm using a static site generator.  I wish I had figured that out earlier instead of wasting time on it.

## Goals for Tomorrow
* Create mind map
* Experiment with Twine

# 9/4/2026
## Mind Map
I created my mind map.  I found a program called XMind that has already built templates for mind maps.  It definitely looks better than anything I could manage in FigJam.  My mind map ended up being a retelling of my presentation that I gave in class.  But I figure this is fine because I already had a lot of details worked out at that point.  I may update it in the future.

![Mind Map](./static/mind_map.png)

## Experimenting with Twine
I also worked with Twine today.  I set up a simple story to test with.  I'm having lots of fun with it.  I worked about an hour with it so far and I didn't want to stop.  I chose to so I could start creating this journal entry.

### Terminology I learned:
* Story
    * The project itself
* Passages
    * These are equivalent to a page in a choose your own adventure book
* Links
    * Point to other passages
* Macros
    * Coding commands such as "set" and "if"

### Coding I worked on:
* Navigation between passages
* Setting Variables
* Using `if/else` statements

### Coding Example
```
{
	(if: (history:)'s last is "Start") [
    	(set: $my_var to "testing")
		]
	(else:) [
    	Variable isn't correct
		]
}
{
	(if: $my_var is "testing") [
		Variable is correct
    	[[Secret Page]]
	]
}
```

**This code does the following:**
* Checks to see if the last passage you were in was called "Start"
    * If it is, it sets a variable called `my_var` to "testing"
    * If it's not, print out "Variable isn't correct"
* Check to see if the variable `my_var` is "testing"
    * If it is, print "Variable is correct" and show a link to another passage
    * Nothing happens if the variable does not equal "testing"

## Goals for Tomorrow
* Experiment more with Twine
* Test hosting ideas (web server, download link, etc)
