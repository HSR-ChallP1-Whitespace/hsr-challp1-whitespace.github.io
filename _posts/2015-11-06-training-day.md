---
layout: post
title: "Training day and presentation"
date: 2015-11-06
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Friday, 06. November 2015

### Introduction
Today we got our first chance to make trainings on a real track. And we found a lot of problems in our algorithm.

### Starterkit connection to track
First we had little problems connecting to Wolfgang's track system, but that was just because we didn't know how the starterkit works without simulator.
You just have to change all URL's in the *application.yml*. (change localhost to correct IP)

And then the trick is to start the application with the following parameters:


{% highlight bash %}
java -jar target/autopilot-{version}.jar -p rabbit -f pilot
{% endhighlight %}

### Trainings
Already in our first training we realized that the algorithm won't recognize the track. It took some minutes until we found out that 
we don't get a round time message. That's a problem because we match the track with this information. To make more usefull trainings 
we changed the algorithm a little, so that we match the track. It was just a quick-fix and no real solution. (works only if there is just one match) But it worked for this track.
After a few changes to our thresholds and constants we had a very good round. We matched the track, we started speeding up, we learned from the penalties, but in the end our 
not existent logic how to speedup in curves throw us out of the track.

After Wolfgang changed the car, we realized that we have to change some constants again because each car is different.

In the end it was a very nice day and we learned a lot.

#### Learnings
There is a lot we have to change:

 - reconsider pattern matching algorithm without round time information
 - consider latency
 - configure algorithm constants dynamically
 - curve logic
 - improve speeding up in straights
 - improve error tolerance in general

### Presentation
After the trainings we did our last preparations for our presentation and at 17:30 we presented to Wolfgang and Markus Stolze what we did until today.
[Here](/media/presentation-06.11.2015.pdf) you can find the slides from our presentation.

