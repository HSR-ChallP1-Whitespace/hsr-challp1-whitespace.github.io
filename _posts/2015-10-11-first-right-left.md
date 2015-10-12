---
layout: post
title: "Right-Left-Straight..."
date: 2015-10-11
categories:
author: "Roberto Cuervo & Stefan Kapferer"
---
## Sunday, 10. October 2015
TODO COMPLETE
### Introduction
After our positive experience with the data visualization, we wanted to extend it with the standard deviation of the gyro z values. So maybe we can better recognize if is a right or left curve, or a straight. Stefan added than a new function:

{% highlight java %}
FloatingHistory smoothedValues = new FloatingHistory(8);

// Sensor event:
double gyrZ = event.getG()[2];
smoothedValues.shift(gyrZ);

// get mean:
smoothedValues.currentMean()
//new function for standard deviation
smoothedValues.currentStDev()

{% endhighlight %}
And there we are with the three curves: blue are the row values, red are the moving average values and new, orange are the standard deviation values:

![Data Analyzer - standard deviation data](/media/data-analyzer_screenshot-04.png "Data Analyzer - standard deviation")

### First curve recognizer
The next step we took, was start trying to recognize curves and straights. This first attempt used only the row data. We fixed a positive and negative threshold, and when the gyro z values are higher or lower, we have a right or a left curve, or a straight. 
This "silly" recognizer worked pretty good, but of course we could not trust it very much. The row values have peaks, and these invalid all the recognition. 

### Second curve recognizer
After exploring the track, we want to know where we are and how fast we can drive. Our approach is, first, split the track in curves or straights. We created a TrackPart class, and a enum:

{% highlight java %}

public enum Direction {
	RIGHT, LEFT, STRAIGHT

}
{% endhighlight %}

This "enhanced" curve recognizer uses moving averages. So we avoid peak values and use the nice red function in our graphs. 
The mechanism is again very simple: we read the values, and when they reach certain thresholds, we create a new instance of the TrackPart class in which we save the direction, start and end times. When the values reach another threshold, we create again the corresponding instance.

{% highlight java %}
public class TrackPart {
	...
}
{% endhighlight %}


We save all these instances in a Track container class, because what we want is...

### Perodicity
Yes, we want to know when a new lap starts. In order to achieve that, starting from all the saved TrackPart instances we create a pattern like: RIGHT - LEFT - RIGHT -RIGHT - LEFT - STRAIGHT - LEFT. See an example:
{% highlight bash %}
TrackPart[direction=STRAIGHT, start=146617, end=150409]
TrackPart[direction=RIGHT, start=150409, end=151037]
TrackPart[direction=LEFT, start=151037, end=151447]
TrackPart[direction=RIGHT, start=151447, end=154197]
TrackPart[direction=LEFT, start=154197, end=155726]
TrackPart[direction=STRAIGHT, start=155726, end=156367]
TrackPart[direction=LEFT, start=156367, end=157348]
TrackPart[direction=RIGHT, start=157348, end=159538]
TrackPart[direction=STRAIGHT, start=159538, end=163808]
TrackPart[direction=RIGHT, start=163808, end=165765]
TrackPart[direction=STRAIGHT, start=165765, end=168578]
TrackPart[direction=LEFT, start=168578, end=170088]
TrackPart[direction=STRAIGHT, start=170088, end=170595]
TrackPart[direction=LEFT, start=170595, end=172108]
TrackPart[direction=STRAIGHT, start=172108, end=173998]
TrackPart[direction=RIGHT, start=173998, end=174557]
TrackPart[direction=LEFT, start=174557, end=175085]
TrackPart[direction=STRAIGHT, start=175085, end=175367]
TrackPart[direction=RIGHT, start=175367, end=177898]
{% endhighlight %}

We compare continuously this pattern with the new ones incoming with each event, if we match, maybe we found the track model. If we found the model, maybe is time to start speeding up!!   
Still we have to check our logic, and oc course, test all.
**Thats all, folks...**
