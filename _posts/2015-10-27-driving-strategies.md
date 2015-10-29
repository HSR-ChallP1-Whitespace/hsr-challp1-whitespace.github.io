---
layout: post
title: "Driving strategies"
date: 2015-10-27
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Sunday, 25. October 2015

### Introduction
Last sunday, we started discussing how to implement a first driving logic. By now were doing fine, speeding up and enjoying the views, but...

### Penalty, penalty, and... oh, yes!, penalty!
Yeah, all was going well... First thing we did after our track recognition worked, was speeding up. But already since the second lap after speeding up, we didn't stop receiving penalties. Yes, we drove fast, with very high velocity. But we received a penalty almost in each light barrier. And we spent a lot of time today to discuss how we could implement a better algorithm.

We draw a lot of tracks and cars, we talked to other students... that was real braining storm!

Also we had to check another "internal" problems too, as we realized that the communication between our actors could be done better. We had some actors that shared references to same objects, which is not the idea of akka. (shared memory should be avoided) Stefan did a great refactoring job. Only this took a lot of time, so we agreed to continue the next day.

## Monday, 26. October 2015
After our monday classes, we resumed the task of finding out the best way to speed up without penalties. We were there, in a commom space at the university, with a lot of students around. Some of our classmates asked what were we doing, and we begun a five head discussion.

There are different idea's... We already started an implementation based on the idea that we speedup on the straight parts and brake down before the next curve. But how much we have to brake down?
First we implemented a solution which brakes down to the initial speed we had before. But with that solution we loose too much time.
Our collegues asked if we could calculate the maximal speed of a curve with physical/mathematical functions using the gyro-data. We thought/googled some time about that idea without finding a solution.
We think that approach gets too complex and we aren't real cracks with physics :-)

Then, one step backwards... We decided to implement a simpler idea first. We improve our track recognition and the model. We store each velocity-barrier in the model.
With the VelocityMessage's we can save which TrackPart has a barrier. This information helps us later to detect the position of penalty message.
Now we just speedup in each straight part. We don't brake down until we get penalties. If we get a penalty we store that information in the corresponding trackpart/barrier.
With this information we could use a smaller power-value in that trackpart in the next round and hopefully don't get a penalty again. If we store that 'maximal power' in each
trackpart we can set the power individually.

We didn't finished the implementation of our idea today, but we hope that we are on a good way. We could have worked more, but at 18:30 we had an appointment with... Rafa Nadal and Rosol, the Swiss Indoors in Basel. A Spaniard can't give up watching Nadal, and Stefan is the tennis freak...

For one time, no graphs:


![Nadal after wining Rosol](/media/nadal.jpg "Nadal after wining Rosol") 

PS: As you can see, Rafa won.
	
**Thats all, folks...**
