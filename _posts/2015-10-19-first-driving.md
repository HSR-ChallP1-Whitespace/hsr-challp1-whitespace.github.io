---
layout: post
title: "First driving"
date: 2015-10-19
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Monday, 19. October 2015

### Introduction
Yesterday we were sure that our PositionCalculator would get lost as soon as we increased the velocity, and we would habe to find another way to recover the position.
Well... it doesn't.

### "We drive, therefore we are"
Finally we can speed up!! We have waited so long for this moment!
But don't get overexcited. We speed up, yes, but at the moment only in straights.
We deliberated long time in order to find a simple approach to this next challenge. How can we drive? Or better said: how can we drive fast?
We know the track, we have a pattern, we have the position and we have the start and end times from each track part or subtrack.
Ok, we will start speeding up as soon as we know that we are in a straight. The PositionCalculator sends a message to our pilot, WhitespacePilot, at each direction change. In this message it sends the current track part and the following track part. 
With this information, the WhitespacePilot speeds up in the straigths.
The obvious question is: when do we stop speeding up? Or: when so we have to brake?
The first solution is using the track part times we collected in the recognition lap. We speed up in the straight during a part of the collected time. After that, we reduce the power to its previous value.

But ,which is this previous power value? We discovered, that if we want to entry in the curves without risks, the best idea is saving the power of each track part during the recognition lap.

I know it is a bit messy, so I will try to explain it from the beginning. You can watch the whole process in the video below.
First, we drive recognition laps with a constant default power value in order to recognize the track. This value is saved with each track part, together with the start and end times, and the direction.

When we have matched the track parts pattern, we try to match when the pattern starts repeating itself. We do this with the round time. As soon as we have this, the PositionCalculator "calculates" the current car position (until this moment we didn't know where were we) and it communicates it to the WhitespacePilot. This starts driving, speeding up in the straigths during a fraction of the track part time, and always reducing the power to the next curve track power value, saved in the track part.

And so on. Watch the video, we know it's still not clear enough in order to understand the whole logic, but it works!
Next steps will be the optimization of this algorithm, with acceleration in the curves, and how react to the penalties we will sure receive.

![First driving video](/media/positionDetection.gif "First driving video")

TODO COMPLETE



**Thats all, folks...**
