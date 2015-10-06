---
layout: post
title: "Research: How can we recognize the track? (and II)"
date: 2015-10-05
categories:
author: "Roberto Cuervo"
---
## Monday, 05. October 2015

Today we have learnt a lot of things, and we opened our minds to new ideas.
After the conversation with the math professor, it seemed clear for us, that the first thing we need is a good data visualization. If we can represent the data as a nice function graph, it will be easier to recognize possible patterns. Also we will be able to see how can we know if we passed the lap/round. Stefan worked hard, and soon we had a first prototype of the function graph.(He explains how it works in its [own post](http://hsr-challp1-whitespace.github.io/2015/10/06/data-visualization.html).

Here a nice image of our first graph!!

![Carrera graph](/media/lap.png "Carrera graph")

As you can see, there are two lines, the blue one and the red one. The blue line is the first line we got, and represent the row data, a.k.a the signal with noise. If we want to recognize the track, know where our car is, and drive, we need to remove the big signal variations. Once more, we remembered what the math professor said about "moving averages", and we did a little research in order to know how could we use this in this context.

And the result: we took the red pill!! The red line is the function graph calculated with "moving averages". You can see that the curve is softer, without big peaks or jumps. And we are able to change the granularity, so we can have an "average curve" with more or less peaks, what we think it will be useful later, at driving.

All this was good, but as usual, when you got some answers, you get more questions too. How can we know where is the car? How can we know when the round starts again?. These questions were still unanswered.

We continue looking at the code... and there it is. We receive the round time!! At the first sight, it should make our life easier. If we have the round time we have less problems in order to know when a new round starts.

This discovery again open new doors. Ok, we have the round time, but, which is the best way to build a track model?. The first idea is driving the first lap with constant velocity, and then calculate the track lenght. At the same time, with the z values we could "mark" left curve, right curve and straight. This idea continues with our approach of 2015-09-30, splitting the track into parts and compare them after. So, after the first round, we would be able to drive faster.
But the difficulty is still, that faster means track recognition again. Because the track is different at higher velocities.

The questions are still a lot. How can we save all this data, process it and at the same time, drive the car? The logic is huge!!

We agreed about working further in this "split" idea, and after looking at the code and making some experiments, we realized that driving the car with constant velocity is almost impossible. We have no direct velocity control, only power control. We need to change our approach... again.





