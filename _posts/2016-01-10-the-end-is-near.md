---
layout: post
title: "The end is near..."
date: 2016-01-10
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Sunday, 10. January 2016

### Introduction
It's a long time since we wrote our last lab-log. We worked hard in the last december weeks to improve our speedup algorithm.
To be honest, without much success... We git a bit in trouble because the logic was too complicated and we had no more time.
Now we have to learn for our exams. We both have a lot of them next weeks...

That's why we decided last week, that we cannot invest a lot more time into the project. We already did more than 240 hours.
But we made some last small improvements during the last week. Without great hopes that it will work in the final tomorrow :-)

### The last few improvements
We made some commit's during this week to improve the algorithm at some points a little bit.
Here we give a short summary over the changes:

 - Driver-Actor Refactoring: made abstract base driver and implemented different drivers for STRAIGHT's and CURVE's (we had a bit too much code in one driver-class)
 - Implemented solution for the problem that we got at the training day, when we configured the initial power value too small
 - STRAIGHT-Speedup: We changed the logic, that we already start speeding up in the curve before a straight part
 - Big Speedup-Logic Refactoring: The logic we implemented in our dark times (december) was just too complex and we lost the overview. We made a big refactoring here and especially made the logic a lot simpler.
 - Fixed some small bugs...
 - Last but not least we tried again to improve the algorithm a little bit (in the simulator we won some seconds, but as we know, real track is something different...)

Thats it.

### Conclusion
That's all for today. Tomorrow is the big final...
We don't expect much, because we don't have a solution which is as good as we wanted :-)
But, lets see how it goes.

**May the force be with us!**

