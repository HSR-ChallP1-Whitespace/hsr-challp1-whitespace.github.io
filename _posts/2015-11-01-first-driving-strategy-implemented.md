---
layout: post
title: "First driving strategy implemented"
date: 2015-11-02
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Sunday, 01. November 2015

### Introduction
Last monday (26.10.) we already made a plan how to implement a first driving strategy... Just speedup in each STRAIGHT part until we get penalties and the brake down a little, to avoid the penalties again.

### Improved position detection
As we wrote in the last post, we store each light barrier in our track model. This helped us to improve our track position detector a little.
When we drive through a barrier we can check if the position is still correct, because we know in which track-part the barrier is. If the position detector is lost (because of the speed or whatever), we can use this to correct the position.

### Implementation of the first driving strategy
We implemented a first driving strategy now, which speeds up in each straight track part. For the moment we don't brake down in the curves. We just hold the speed from the straight part.
We do that until we get a penalty. We store the penalty in the model (corresponding track-part) with the power-value we had on that part.
Next time we come to that part we reduce that power a little in order to avoid getting the penalty again. (we repeat this until we don't get the penalty anymore)
The very-first idea was to brake down before the curves to the initial speed. But we found out that this idea cost's a lot of time. We can also drive faster in the curves. (How much is another question :-))

After we implemented the strategy we tested it and saw that there is one big problem with it.
There are small straight parts without barriers. In these you never get a penalty. And we don't brake down in the following curves, so we enter them with maximum-power after some rounds.
The simulator doesn't care about this, but we think that it would't work in reality. 

Another problem: After some speed increases, our position detector gets totally lost. The position is no longer correct.
Whats the mistake? A question we must postpone to tomorrow. It's enough for today.


## Monday, 02. November 2015
After a recovering night we can start to solve our problems.

I solved the problem with the position detection in the train, on my way to school. The problem was our threshold of the standard deviation we defined 
for the detection of the straight track parts. 

I solved it with a little change of the threshold: 

[https://github.com/HSR-ChallP1-Whitespace/autopilot/commit/bff2f6a5f66e7868ebfaa2c57550e5de285b5b4a](https://github.com/HSR-ChallP1-Whitespace/autopilot/commit/bff2f6a5f66e7868ebfaa2c57550e5de285b5b4a)


We also found a solution for the other problem with the small straight parts without barriers. For the moment we just stop speeding up when the length (time) of the part gets smaller than a defined threshold.
With more speed, the time saved in the trackpart gets smaller. If it's too small, we just hold the power as it is.

After some tests we saw that the strategy works for most of the tracks of the simulator: 

 - we speed up
 - we get penalties
 - we reduce the power a little
 - we drive without penalties after some rounds

With this strategy we are faster. Of course... (otherwise something would be very wrong)

We always check how much faster we get with the round times:

![Round times](/media/first-driving-strategy_round-times.jpg "Round times")

That's it for the moment. It works, but...

... still we have the feeling that this is very slow... We somehow need to figure out how fast we can drive in the curves.
And I think we have to improve the strategy in long straight parts. (speedup in the beginning and brake down before the curve for example)

**That's all for today.** We are looking forward to friday where we can test what we have on the real track.



