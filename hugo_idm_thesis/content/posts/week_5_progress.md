---
title: "Week 5 Progress"
date: 2026-10-02T09:28:59-04:00
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

# This Week's Schedule

| Day | Game / Project | Paper / Research | Journal / Class |
|---|---|---|---|
| **Fri 10/2** | Review current Twine build. Make a **must work for critique** vs. **nice to have** list. | Review revised outline. Treat new RQ as working question. Process **1 source** and capture notes in Zotero. | — |
| **Sat 10/3** | Work on core midterm mechanics, prioritizing **apartment navigation + inventory**. Test as you go and document development decisions/problems for Methods. | Process **1 source** and identify which Lit Review pillar it supports. | — |
| **Sun 10/4** | **OFF / BUFFER** | **OFF / BUFFER** | Rest! |
| **Mon 10/5** | Continue must-work-for-critique features. Test navigation and inventory together. | Begin **Introduction** draft. Draft RQ section if ready. Begin thinking through revised Hypothesis/guiding proposition. | — |
| **Tue 10/6** | Test Wednesday's demo. Fix anything blocking meaningful critique. Decide what to demonstrate. Review presentation and prepare specific critique questions. | Process **1 source**. Continue writing only if time/energy allows. | Begin/complete **Production Process journal**. |
| **Wed 10/7** | Quick demo test. **No last-minute feature creep.** | — | **PRE-DEMO / PRE-MIDTERM CRITIQUE.** Get feedback on project, presentation, and demo. Record feedback. |

# 10/2/26

## Game Prep for Pre-Demo Day Critique

### Need to Have

* Inventory System
  * Ability to pick up objects
  * Objects should appear in inventory

* Navigation
  * Ability to move between apartment locations
  * Short description (prose) of each location
 
### Nice to Have

* Inventory System
  * Easy to read/nice visuals
  * Ability to drop objects (will eventually be Gwen giving Avery things)
  * No link to pick up an object if it's already in the inventory

* Navigation
  * Links to locations update to say if the player has already been there
  * Location description changes after location visit 

# 10/3/26

## Creating Links to Pick Up Items

I found the `link:` macro in Harlowe today.  It creates text that looks the same as what is used to navigate between passages.  You can use these to change text, set variables, and navigate.  There are also link-based macros that can combine two macros in one.  There is a similar macro called `click:` that makes it easier to separate prose and code for a cleaner backend.

See [this documentation](https://twine2.neocities.org/#macro_click) for more information.

This test has a passage that details a living room with a remote control on a table.  The code checks for a variable called `$hasControl` which initializes as `false` at the beginning of the game.  If the variable is set to `false` it shows a link to "Pick up the remote control".  If it's `true` the passage will say, "There's nothing to pick up here" to keep the player from trying to pick it up twice.

When the player clicks on the link it will add another item (the remote control) to the inventory array.  This is a step further from the last tech demo where I had the game append items to the array on its own through code.

The current tricky part is that I have to learn how to dynamically update the inventory in the footer.  When then players picks up an item, the inventory should display it.  I'm looking at the `re-run` macro and `replace` macro to try and get this to work.

![Living Room Code - Pass 1](living_room_code_1.png)

![Inventory Code - Pass 1](inventory_code_1.png)

Currently this isn't working as it should.  But I was able to verify that `$hasControl` was set to `true` and the item was appended to the array when the link was clicked.

![Debug Window Before Clicking](click_debug_before_1.png)

![Debug Window After Clicking](click_debug_after_1.png)
