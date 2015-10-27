---
layout: post
title: "Lost & Found"
date: 2015-10-27
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Sunday, 25. October 2015

### Introduction
Last sunday, we just got lost. We were doing fine, speeding up and enjoying the views, but...

### Penalty, penalty, and... oh, yes!, penalty!
Yeah, all was going well... but already since the second lap after speeding up, we didn't stop receiving penalties. Yes, we drove fast, with very high velocity. But we received a penalty almost in each light barrier. And we spent in this way the whole afternoon trying to find out, how could we avoid this.

For us it was clear, that our "drive logic" was not working properly. But, how can we drive fast and not receive penalties? "To be, or not to be, that is the question" (Maybe there is no relation between penalties and Hamlet, but who cares...).

We discussed a lot as usual, we drow a lot of tracks and cars, we talked to other students... that was real braining storm!

We had to check another "internal" problems too, as we realized that the communication between our actors could be done better. Stefan did a great refactoring job, and after that our actors could play Hamlet without problem. Only this took a lot of time, so we agreed to continue the next day.

## Monday, 26. October 2015
After our monday classes, we resumed the task of finding out the best way to speed up without penalties. We were there, in a commom space at the university, with a lot of students around. Some of our classmates asked what were we doing, and we begun a five head discussion.
It went not very long, and in fact we found no good solution.
But after, as Stefan and I were talking about a classmate's idea, we realized that we had to start again from zero.

Then, one step backwards. ...Ok, we have the track pattern, we have the track parts, we have our current position... but we have no idea about when we can speed up and when not. Or how much we can speed up.

But we have neither the velocity, or the track length. We conclused, that we had to find the upper velocity boundary. And how? 

Penalties, of course!!

When we receive a penalty, we know that we are too fast. So when we receive one, we save the current power of the current track part, and the next time, before entering this track part, we know the maximal power we can give. 
We save also the light barrier position, in this way we have complete information about the track part.

But finding out where are the ligth positions is not an easy task, and we spent good part of the afternoon with this. We could have worked more, but at 18:30 we had an appointment with... Rafa Nadal and Rosol, the Swiss Indoors in Basel. A Spaniard can't give up watching Nadal, and Stefan is the tennis freak...   

For one time, no graphs:


![Nadal after wininng Rosol](/media/nadal.jpg "Nadal after wininng Rosol") 

PS: As you can see, Rafa won.
	
**Thats all, folks...**
