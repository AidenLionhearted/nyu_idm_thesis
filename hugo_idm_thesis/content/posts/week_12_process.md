---
title: "Week 12 Process"
date: 2026-11-22T08:26:12-05:00
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

# 11/22/2026

## Post-Playtesting Improvements

### Content Warnings

I decided to make the content warnings more specific around the themes the game contains.

I also edited the title screen to say that the game includes themes of grief and loss.  Those topics are broad enough that I don't believe they are spoilers.  I also wrote that the content warnings page will contain spoilers.  I'm not sure if this is the best way to implement it.  But I think it's a good idea.


Title Screen
```
Hello Player,

You are about to experience the story of Gwen and their friend Avery.

This game explores themes of grief and loss.  
If you would like more detailed content warnings, click the link below.  
They do contain spoilers.

You will be able to start the game from here and from the content warnings page.

[[View Content Warnings->content-warnings]] 
[[Play->intro-1]]
```

Content Warnings Page
```
This game has themes of:
* Death
* Depression
* Disenfranchised grief
* Grief from loss of ability
* Pet loss

Disenfranchised grief is when others do not see the person's grief as legitimate or worthy of feeling.

[[Play->intro-1]]
```
# 11/25/2026

## Post-Playtesting Improvements

### Dedication Page

I thought that making a dedication page would take 15 minutes tops.  But of course I didn't take into account the time I needed to make it look good.

I started by making the dedication it's own passage.  But Twine doesn't support automatically going to another passage with a delay.  The macro `go-to` is immediate.  The only other option would be to apply transitions to links, but that's not what I wanted to do.

So the dedication page is in the same passage as the "And I breathe" passage.  I discovered the `after` macro that performs the code it's attatched to after a specified amount of time.  I also used `replace` to replace the "And I breathe" hook with the dedication hook.

```
{
	(align:"=><=") + (transition:"fade") + (transition-time: 3s)|breathe>[And I breathe.]

    (after: 5s)[
    	(align:"=><=") +  (transition:"fade") + (transition-time: 5s) + (replace: ?breathe)  \
        [<img 	src="gwen.jpg" alt="Picture of my dog, Gwen" width="378" height="504">
		<br>
		In Memory of Gwen<br>
		July 25, 2010 - June 27, 2025]
	]
}
```

