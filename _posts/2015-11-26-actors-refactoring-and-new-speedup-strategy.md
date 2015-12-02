---
layout: post
title: "Actors refactoring and new speedup strategy"
date: 2015-11-26
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Thursday, 26. November 2015

### Introduction
A long time since we wrote our last lab-log... Time to summarize up what we did the last days:

 - sunday, 22.11.2015
 - monday, 23.11.2015
 - thursday, 26.11.2015

### Fixed little problems with new track recognition
Last sunday (22.11.) we fixed some little problems with our new track recognition.
Now it works very well. (at least it looks like that :-))

With the 'levenshtein distance' we also check now a lot more patterns which maybe have only small mistakes.
For each pattern we create a new actor. This actor tries to confirm that the pattern is correct with the following GYR-Z data.
Of course we also check a lot of patterns which doesn't make sense, but it doesn't cost us very much. We produce a lot of different
patterns which are **maybe** correct. But the logic works well because afterwards the actors only confirm a pattern if it matches 
100% with the following data. (We just need two rounds which create the same pattern. Should be possible with constant power...)

**TODO:** We will now see how it works. Maybe we have to add some additional logic which reset's all the data after some time, if
we really don't match anything. (start from scratch)

### Actors refactoring
We did a big refactoring in our model and in our actors. Our old solution based on one actor which drived in all track parts.
We had the trackparts in our model, but we had to store a lot of driving-data in that model.

**Another problem we had:**
The data we needed in the *track recognition* where different from the data we needed in the *position detection* and while *speeding up*.
That's why we started implementing different models for different *driving stages*.

Wolfgang gave us a little tipp in our presentation (06.11.2015) which can make the code a little easier.

We are now back to just one single model. That model just represents the track with it's trackparts, independent of the *driving stage*.
The data we need for the different *stages* are managed by actors. After we matched the track we create an actor for each trackpart. 
Every actor is responsible for driving in it's own trackpart. All data which the actor needs for that are now stored in the actor, and not
in the track model. Makes things a little easier there...

### New speedup logic/strategy
We discussed a lot in the last days how we could implement a new strategy for speeding up. Since the training day we knew that our 
current strategy is not useful in the end. We just speeded up in each trackpart until we got penalties. But we have to implement a solution 
which speeds up in the beginning of straight parts and brakes down in the end... But how do we know, how much we have to break down.? 

How can we measure the effectiveness of our brakings? We need a solution where we can speedup and detect how much (and when) we have to brake.
After a lot of discussion and brainpower we had an idea. We can use the timestamps of our trackparts. Each time we enter and we leave a trackpart 
we store a timestamp. With that information we can calculate the duration's we had for each trackpart. If we speedup in straight parts and brake in the end, we 
can measure the brake effectiveness with the duration of the following trackpart(s). If the duration is smaller we were faster, otherwise we were slower.
With that data we can try to optimize the speed in the straight parts and try to drive into the following curves always with the same speed.

Another idea: We maybe should only optimize one straight part at a time. And after we optimized that one, we take the next, and so on... 
That makes things easier because we have less influences from other trackpart's which are also speeding up. (different speeds when entering trackpart)

#### Conclusion 
Now we have a lot of idea's how to implement a new strategy. The next step will be to start implementing these idea's and make experiments with the simulator.
Again we will focus on the straight parts in the new strategy. We can do that a lot better as we did before. The curves are another problem. (I think
we will never find a good solution for that :D)

So... Thats all for today.
We will let you know how our experiments proceed in a few days.

