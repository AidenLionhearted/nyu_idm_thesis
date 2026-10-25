---
title: "Week 8 Progress"
date: 2026-10-25T14:00:59-04:00
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


# This Week’s Schedule

| Day | Game / Project | Paper / Research | Journal / Class |
|---|---|---|---|
| Thu 10/22 | **OFF / REST** | **OFF / REST** | Recover from Demo Day, anxiety, and doctor's appointment. |
| Fri 10/23 | Continue game script: living room exploration and first object. | No required paper work. | Optional development notes. |
| Sat 10/24 | Optional kitchen scene after yard sales, Goodwill, and lunch with Dad. | **OFF / BUFFER** | Rest or optional reflection. |
| Sun 10/25 | Main writing session: bathroom and bedroom scenes, Gwen's realization. Two 45–60 minute sessions with a break. | No required paper work. | Optional notes on narrative decisions. |
| Mon 10/26 | Write the ending involving the stray dog and Avery. | No required paper work. | Record story development notes if useful. |
| Tue 10/27 | Light script review, if energy permits. | Optional Methods notes. | Eye doctor appointment. Light workload. |
| Wed 10/28 | Review game progress and identify next steps. | Prepare questions about remaining paper work and playtesting. | **ONE-ON-ONE WITH VANESSA — 6:30 PM ET.** |

# 10/25/26

## Script Writing Progress

I continued writing the script for the game this week.  I hadn't touched it in a long time.  Honestly, it was one of the scariest parts of this project because I assumed that my writing would be so concise that it would take only a couple minutes to read and play the game.  But I needn't have worried because once I got started I got in a good flow.

Once I gave myself permission to not write the script perfectly the first time I was able to just write and not spend forever trying to decide what to write.  I decided to write the script inside my thesis paper Google doc.  I like the tab system because I am able to split up the writing sections into events and locations.  If I wrote directly in Twine it would be a bit harder to track where everything is and the writing might get a little buried with Harlowe code.  My structure looks like this:

![Tab structure for the script](script_tab_structure.png)

Each location has flavor text that the player sees when navigating to that location.  There is a before object pick up and after object pickup version.  It also includes Harlowe syntax hooks for navigating to different areas and picking up objects.  This will make it easier to keep track of all the passage links when I import it into Twine.

![Kitchen tab](kitchen_tab.png)

![Frisbee tab](frisbee_tab.png)

I also started questioning my inventory system.  Since Gwen is a dog, she can't carry more than one thing at a time.  So it made me question my use of an inventory.  Why have one if you can only store one object at a time?  But I decided to keep it because at least the player knows what they're carrying and has that context when bringing the items to Avery.

I also wrestled with the actual carrying.  Can spirits carry objects?  Will the big reveal of Gwen's form as a spirit undermine this?  I decided it didn't.  This is a game and I believe the player won't question the "supernatural rules".

Then there's the aspect that Professor Ansari asked about during my midterm presentation.  Do the objects influence the story?  Do they just provide lore?  I considered maybe doing branching paths after all.  Or limiting how many times the player can gather an object and having to choose wisely.  But I'm staying strong on my scope guidelines.  No branching paths.  No complicated new mechanics.  Like Professor Duff suggested, I'm going to focus on the narrative.  Does that make this a walking simulator type game?  Maybe.  But that's okay.  There have been amazing games like What Remains of Edith Finch that are essentially walking simulators.  

I do plan on making a tracker variable that stores how many times Gwen has tried to interact with Avery and depending on that variable the prose when going to the bedroom is different.  With each attempt to get to Avery, the more Gwen starts realizing something is wrong with her.  This will have a scope too.  This variable won't change the text in the other locations.  While I could do that, it'll take substantially more time that I don't really have at this point in the semester.  So the only prose that changes is the bedroom.  After getting the last object, the door to the bedroom will open, Gwen will finally go inside, and she will see Avery crying while holding Gwen's collar.  That's the reveal.

So this week has been script heavy and I intend to post more this week depending on how that process goes.
