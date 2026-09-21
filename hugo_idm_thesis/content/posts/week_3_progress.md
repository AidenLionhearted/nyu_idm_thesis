---
title: "Week 3 Progress"
date: 2026-09-17T15:06:50-04:00
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

# 9/17/26

## Revised Schedule

I worked with ChatGPT today to synthesize the notes from my one-on-one, the rubric sent out this morning, and the original class schedule to make a new planning document.  This was absolutely necessary because my original one did not have all the information to make it accurate.  I did coach ChatGPT to fix errors, rewrite confusing parts, and use the columns that I wanted to create a table.  I have stored this table inside my thesis Google Doc with a ChatGPT acknowledgement in bold at the top.

I'm so happy to have this because it makes the workload less intimidating and easy to chunk across the week itself.

This is the schedule for this week specifically.

| Date         | Focus                       | Plan                                                                                                                                                                                                                                            |
| ------------ | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Thu 9/17** | 📚 Research                 | Continue the interactive-narrative article you're already working through. Take useful notes, especially anything relevant to interaction/choice/narrative design. If energy permits, identify the next source to read.                         |
| **Fri 9/18** | 🎮 Prototype                | Work in Twine. Continue the script/current passages and choose **one useful thing to experiment with** for next week's prototype. The goal is something you can show, not a polished chunk of the final game.                                   |
| **Sat 9/19** | 📝 Outline + light research | Create the annotated-outline document and put in all required paper headings. Start rough notes/descriptions under the sections you already understand. Look through your old independent-study readings and flag potentially relevant sources. |
| **Sun 9/20** | **Buffer / off**            | No required thesis work. If something slipped earlier, this is available as a catch-up day—but I would rather preserve it as breathing room.                                                                                                    |
| **Mon 9/21** | 🎮 Prototype                | Main prototype work session. Get whatever you're showing Wednesday into demonstrable shape. Test it yourself and make notes about what worked, what didn't, and what questions you want feedback on.                                            |
| **Tue 9/22** | 📚 + 🎮 Wrap-up             | Process another research source if feasible. Do a **final prototype check**, make sure your Twine build/link works, and prepare a few points about what you experimented with and what feedback you want. No major new features Tuesday night.  |
| **Wed 9/23** | 🎓 Class                    | **Show prototype.** Get feedback. After class, Week 4 begins and we switch to the next row of your project plan.                                                                                                                                |
## Literature Research

This journal is explicitly for the progress of the game development itself.  I will not be discussing any of the literature that I am reading here unless it impacts design/development choices.

## Future of this Journal

I might not be posting in here every day.  Some days might be dedicated solely to paper related work and on those days I won't make an entry.

## Goals for Tomorrow

* Continue the script for the game
* Start porting the passages into Twine 

# 9/18/26

## Porting to Twine

I put all my existing script into Twine.  I'm naming the passages using hyphens instead of underscores because Twine considers underscores code related.

The title screen and the content warning passages both point to `intro-gwen-1` which is the first passage of the game.  Each paragraph of the script was given its own passage.  Each passage points to the next one.

![The Twine Passage Map](twine_build.png)

![Title Page Passage Editing Box](passage_box.png)

## Testing CSS Code

Harlowe has a whole library of macros.  These are like functions you can use in your passages to do all sort of things.  It can set variables, add style to different elements, and do things like save and load your game state.

I tried using an enchantment.  Enchantments are a type of changer that applies style to various elements of a passage.  See documentation [here](https://twine2.neocities.org/#macro_enchant).

I put a border around the passage but there was no way to give it padding so it touched all the text.

![Tight Border around Passage](tight_border.png)

After some Google searching I found that the Twine application has a window for global stylesheet overrides.  I was able to add padding to the passage element and a border!

### CSS Code

```
tw-passage {
  border-style: groove;
  padding: 10px
}
```

![Passage with Padded Border](padded_border.png)

## Goals for Next Development Day

* Further explore CSS elements
* Write 2 - 4 story beats and add them into Twine

# 9/21/26

## Harlowe and CSS Experimentation

I wanted to start working on the inventory element so that I had something extra to show in class on Wednesday.  I learned about the special header and footer tags.  This allows you to create a special passage with one of those tags and it will apply to every passage in the game without having to go in every passage and add the code.  Very useful.

I used this video on YouTube to learn about how to code this in Twine: [Video Link](https://www.youtube.com/watch?v=jIhBon_8aM8)

Once I had the special passage set up I ran into an issue where the footer was showing right up against the links at the bottom of the passage.

![Footer Appearing Stuck Next to Links](stuck_footer.png)

So I did some digging and found out that you can use CSS for the footer by adding the `tw-include[type="footer"]` class.  This required multiple iterations of adding new elements to make things look the way I wanted them.

| CSS Code                            | Explanation                                                              |
|-------------------------------------|--------------------------------------------------------------------------|
| display: block                      | Adds line break and takes full width of parent                           |
| margin-top: 20px                    | Adds spacing from the top of the class                                   |
| margin-left: -10px                  | Subtracts 10px to override the parent's padding                          |
| margin-right: -10px                 | Subtracts 10px to override the parent's padding                          |
| padding: 10px                       | Adds padding inside the footer class                                     |
| border-style: groove none none none | Adds a border to the top only                                            |
| font-size: 0.8em                    | Makes the font smaller while being able to be scaled by browser settings |

![Newly Styled Footer](new_footer.png)

I also added another class to the CSS stylesheet so that the footer doesn't appear in passages that I tagged `no-footer`.  So far, those passages are the title screen and the content warnings screen.

![The Tags Menu on the Title Screen Passage](tags.png)

This is the current version of the CSS stylesheet.

```
tw-passage {
  border-style: groove;
  padding: 10px
}

tw-passage[tags~="no-footer"] tw-include[type="footer"] {
  display: none
}

tw-include[type="footer"] {
  display: block;
  margin-top: 20px;
  margin-left: -10px;
  margin-right: -10px;
  padding: 10px;
  border-style: groove none none none;
  font-size: 0.8em
}
```

## Inventory System

I moved on to working on the actual code for the inventory system.  I created a new passage called `starting-variables` and initialized an empty array (`inventoryArray`) to use for items the player collects.  This passage has the special tag `startup` which tells Twine to only use this passage once when the game starts.

This is the starting-variables passage

```
(set: $inventoryArray to (array:))
```

Next I needed to actually build the inventory system.  This code went into the footer passage mentioned above.

The code checks to see if the inventory array is empty.  If it is, it displays the text "Empty".  This is so there isn't a random empty space after the "Inventory:" text.

If the array isn't empty, it loops through each item in the array and prints each item separated by a line break.  The exception is if the item is the last in the array.  Then it ommits the line break so that it doesn't create an empty line at the end.

This is the inventory passage (footer):

```
Inventory:
(if: $inventoryArray is an empty)[Empty]
\(else: ) + (for: each _item, ...$inventoryArray)[_item(unless: _item is $inventoryArray's last)[<br>]]
```

To actually add items to the array, you combine the current array and the new item within the individual passage where the player gets the item.

```
(set: $inventoryArray to it + (a: "Bag"))
```

Right now I am adding random items within the introduction passages.  This is only for testing.  The actual game will add items as the player explores the apartment.

![Empty Inventory](empty_inventory.png)

![Inventory with One Item](one_item_inventory.png)

![Inventory with Two Items](two_item_inventory.png)

## Goals for Next Development Day

* Write 2 - 4 story beats and add them into Twine
