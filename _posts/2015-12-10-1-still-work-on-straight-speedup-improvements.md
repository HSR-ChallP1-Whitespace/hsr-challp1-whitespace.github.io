---
layout: post
title: "#1 - Still working on our straight speedup improvements"
date: 2015-12-10
categories:
author: "Stefan Kapferer"
---
## Thursday, 10. December 2015

### Introduction
Soon it is january and we still have a lot of problems to solve :-/
Time is running out... We worked hard on improvements in our speedup logic for the straight parts.

### What have we done last days...

#### Speedup one straight part after the other
In the beginning of the project we located some problems when speeding up in all parts at the same time.
It's difficult then to optimize because the speedup of one part affects the others.

Thats why we implemented a logic which takes one straight part after the other. If that one is optimized, 
we take the next one. (of course we have to change parameters in the old one too, if the entry-speed changes...)

Maybe we have to think about this again, later. Because we need a lot of rounds with that mechanism, until we have 
optimized all the parts...

#### Give full power (255) in each straight part
We give full power in the beginning of each straight trackpart. With that approach, we only have to optimize 
how long we do that and how much we have to brake down after that.

At the moment we start with a factor of *0.1* of the last trackpart duration. Each round we increase the (full-power-) time 
a little. When our time in the next trackpart gets smaller, we know that we got faster, and we brake more.

#### Current state
We still have to work on the idea described above. The first tests doesn't look very bad, but it's very tricky to always 
calculate the correct *time-until-we-brake* and the *brake-down-power*.

### Next steps
 - we still have to work on our logic and improve it
 - we have to start speeding up already in the curve before the straight part
 - speedup in curves too --> and then make shure that the straight parts adapt
 - ...


That's all I can write for today. We are still working hard and will write a lab-log again, as soon as we know more...

### Update:
There is another problem we had to solve today. I wrote about it here: [#2 - Dubai](/2015/12/10/2-dubai.html)







