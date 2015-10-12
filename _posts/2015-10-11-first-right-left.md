---
layout: post
title: "Right-Left-Straight..."
date: 2015-10-11
categories:
author: "Roberto Cuervo & Stefan Kapferer"
---
## Sunday, 11. October 2015

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
TrackPart[direction=STRAIGHT, start=0, end=3677]
TrackPart[direction=RIGHT, start=3677, end=4238]
TrackPart[direction=LEFT, start=4238, end=4666]
TrackPart[direction=RIGHT, start=4666, end=7469]
TrackPart[direction=LEFT, start=7469, end=8966]
TrackPart[direction=STRAIGHT, start=8966, end=9598]
TrackPart[direction=LEFT, start=9598, end=10568]
TrackPart[direction=RIGHT, start=10568, end=12727]
TrackPart[direction=STRAIGHT, start=12727, end=16945]
TrackPart[direction=RIGHT, start=16945, end=18936]
TrackPart[direction=STRAIGHT, start=18936, end=21628]
TrackPart[direction=LEFT, start=21628, end=23158]
TrackPart[direction=STRAIGHT, start=23158, end=23636]
TrackPart[direction=LEFT, start=23636, end=25195]
TrackPart[direction=STRAIGHT, start=25195, end=27195]
TrackPart[direction=RIGHT, start=27195, end=27726]
TrackPart[direction=LEFT, start=27726, end=28245]
{% endhighlight %}

We compare continuously this pattern with the new ones incoming with each event, if we match, maybe we found the track model. If we found the model, maybe is time to start speeding up!!   
Still we have to check our logic, and oc course, test all.
**Thats all, folks...**
