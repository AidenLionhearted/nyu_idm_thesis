---
title: "Week 9 Progress"
date: 2026-10-29T12:08:24-04:00
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
| Thu 10/29 | Write third bedroom visit and climax. | Add explanations for 2 existing sources. | Record one-on-one feedback and narrative decisions. |
| Fri 10/30 | Draft falling action and ending; send playtesting survey to Vanessa and Ahmed. | — | Document playtesting preparation. |
| Sat 10/31 | Finish narrative draft; begin Twine implementation. | — | Note implementation decisions. |
| Sun 11/1 | Implement remaining passages and item logic. | Add explanations for 2 existing sources. | Evening off. |
| Mon 11/2 | Complete playable build; test all paths. | — | Record technical issues and fixes. |
| Tue 11/3 | Incorporate survey feedback; send invitations if cleared. | Add explanations for 2 existing sources. | Short session; note testing setup. |
| Wed 11/4 | Begin playtesting if cleared; check links. | Add final source explanation; select source 19. | Rest / buffer. |

# 10/30/26

## Creating Playtesting Survey

I created my playtesting survey.  It’s actually more comprehensive than I thought it would be.  The arrangement of the questions made sense.  I also discovered that you can make sections.  Somehow I didn’t see that when I created my research survey last semester.

I think one of the best things is that I did a bit of branching.  The very first question is in its own section and asks the participant if they’ve played the game.

If they answer “Yes”, they’re taken to the complete survey.

If they answer “No”, they’re taken to another section that thanks them for their participation but says they can’t complete the survey if they’ve never played the game.

If they answer “Yes, but I didn’t finish”, it takes them to a different section that asks why they didn’t finish the game.  There are multiple checkboxes they can select along with an “Other” box.

Another branching point is a question that asks the participant how long they have been playing video games.

If they answer any of the time ranges they move onto the next section that asks questions to build a gamer profile.

If they answer “This is my first game” they skip the profile section since they wouldn’t be able to answer those questions.  It could cause enough friction where they don’t want to complete the rest of the survey.

After that I have sections on UX/Usability, story and narrative, and a closing section where participants answer if they’d recommend the game.  There is also a space to write additional feedback.

It took a bit of work but I think it strikes a good balance of types of questions.  Hopefully it doesn’t take too long to answer and people won’t quit early.

# 11/1/26

## Script Writing

I finished the script last night.  It was really cathartic to finish it.  I'm really enjoying the layers that the story has between Avery's grief, Gwen's grief, and the reveal towards the end.

I think my favorite part is the very end.  The last passage.  It says, "And I breathe."  You don't get to know if Avery adopted the stray dog.  You don't know if Avery will be able to manage their grief.  Neither does Gwen.  But she takes a breath.  She made meaning out of her grief.  Even when everything was hopeless.  Even when she suddenly lost her purpose.  She's able to breathe.

And I think that's an important message to send to someone who is moving through grief.  There's no guarantee that you'll find love or happiness right away.  And grief isn't linear and it’s never truly gone.  But being able to breathe, that’s important.  You can move forward despite the uncertainty.  I'm waxing poetic here but it's something I genuinely believe.

## Importing into Twine

I started importing the script into Twine.  I learned a few things while I was working on the importing.  You can use the toolbar in the passage windows to change text color.  It writes the hook for you.  In fact, there's a whole menu to set up different macros and coding without having to write the code.  And I feel silly and like I wasted a lot of time struggling with Harlowe and Twine in past weeks.  But I suppose knowing how to code makes things easier when you need to troubleshoot.

If you get annoyed by line wrap in the passage editor, use the escape character `\` at the end of the line and press enter, the next word will automatically indent to match the first line.  I feel so much better now.

# 11/2/26

## More Importing and Handling Bedroom logic

I continued working on importing my script into Twine.  And in doing so found some wrinkles in the if/else logic that I had to fix.

I have two variables that matter in this context.  One is `$inventoryArray` and the other is `$bedroomAttempts`.  

The inventory array is what holds the objects that Gwen picks up.  You can see its contents in the footer of the game that shows the inventory.
The `bedroomAttempts` variable keeps track of how many times the player has visited the bedroom.  This is important because each time Gwen goes to the bedroom, she gets more and more anxious about Avery not responding to her.

Here's the rub.  If the player goes to the bedroom without ever having been there (bedroomAttempts = 0) and their inventory is empty, it shows a passage about giving Avery some space.  This changes the bedroomAttempts variable to 1.  Since the player has been there once.

> Avery has a lot of great things in their bedroom.  Comfy blankets, their gaming console, stuff like that.
>
>I walk to the bedroom but the door is still closed.  Maybe I should give Avery some space.

But what happens if the player doesn't go there first and goes and picks up an object elsewhere?  The attempts variable is still 0 but their inventory array isn't empty.  The player would be at the bedroom but it wouldn't display anything because there is no `if-else` statement to account for that combination.

So I changed the conditional from the player has been there once and their inventory isn't empty to if the player has been there 1 or fewer times and their inventory is not empty.

> I can hear Avery inside.  They’re crying loudly.  I knock on the door and there’s no response. Maybe they can’t hear me over their crying?  I wait>a couple minutes to see if they’ll open the door.  Still nothing.  I call through the door that I have the <item>.  But Avery continues to cry.
>Maybe something else will help.  I put down the <item> and go to find something else.

And this is fine.  Gwen is worried but hasn't started panicking.  But now we have another condition.  If the player has been to the bedroom at least once and their inventory is empty.  I've written it so that the prose displays, "I need to search the apartment and find something else that could help."  I suppose that works.  It's brief but it's something.  I also had to add logic to empty the array after going to the bedroom because Gwen puts down the object so she can get another one.

Here is the code so far.  It's not finished yet.

```
{
	(if: $bedroomAttempts is 0 and $inventoryArray is an empty)[
    	Avery has a lot of great things in their bedroom.  Comfy blankets, their gaming\
        console, stuff like that.<br><br>
        I walk to the bedroom but the door is still closed.  Maybe I should give Avery\
        some space.<br><br>
        I'll look somewhere else for something to help.<br><br>
		[[Search the living room->living-room]]<br>
		[[Search the kitchen->kitchen]]<br>
		[[Search the bathroom->bathroom]]
        (set: $bedroomAttempts to 1)
	]
	(else-if: $bedroomAttempts <= 1 and $inventoryArray is not an empty)[
    	I can hear Avery inside.  They’re crying loudly.  I knock on the door and there’s no\
    	response. Maybe they can’t hear me over their crying?  I wait a couple minutes\
        to see if they’ll open the door.  Still nothing.  I call through the door that I have the\
        (print: (lowercase: $inventoryArray's 1st)).  But Avery continues to cry.  Maybe\
        something else will help.<br><br>
        I put down the (print: (lowercase:$inventoryArray's 1st)) and go to find something\
        else.<br><br>

		[[Search the living room->living-room]]<br>
		[[Search the kitchen->kitchen]]<br>
		[[Search the bathroom->bathroom]]
        (set: $inventoryArray to (a:))
        (set: $bedroomAttempts to 2)
	]
    (else-if: $bedroomAttempts is 2 and $inventoryArray is not an empty)[
    	Avery’s crying has mostly subsided.  I knock on the door again.  Still no reply.  I call\
        out and ask if they’re okay.  Avery doesn’t respond.  But they always respond to\
        me when I try to get their attention.  Something is wrong.  This is wrong.  I knock\
        again, hoping that maybe this time it’ll be different.  But it isn’t.  I feel my heart\
        beating fast, my breath quickening.<br><br>
        I drop the (print: (lowercase: $inventoryArray's 1st)).<br><br>
        One more try.<br><br>
        
		[[Search the living room->living-room]]<br>
		[[Search the kitchen->kitchen]]<br>
		[[Search the bathroom->bathroom]]
        (set: $inventoryArray to (a:))
        (set: $bedroomAttempts to 3)
    ]
   (else-if: $bedroomAttempts is 3 and $inventoryArray is not an empty)[
    	When I return I’m surprised to see the door to the bedroom open.  Maybe Avery\
        is feeling better already?  I put down the \
        (print: (lowercase: $inventoryArray's 1st)) and slowly walk into the room.  \
        As if walking in too suddenly might startle them.<br><br>
        [[Next->climax-1]]
    ]
   (else-if: $bedroomAttempts >= 1 and $inventoryArray is an empty)[
    	I need to search the apartment and find something else that could help.<br><br>
        
        [[Search the living room->living-room]]<br>
		[[Search the kitchen->kitchen]]<br>
		[[Search the bathroom->bathroom]]
	]    
}
```

Other than all this, the only other thing that I want to change for now is the passage links that say "Bring what I’m holding to Avery".  Because the player might not be holding anything.  And that text wouldn't make sense.  So I'm probably going to change it to somethiing like, "Go to the bedroom".  I don't super like it because the other links say "Search the <location>" but Gwen isn't going to the bedroom to search since the door is closed.  But maybe it's okay.  If I do use the phrase "go to" I'll probably put it as the bottom link so it doesn't look weird being between the ones that say "search".