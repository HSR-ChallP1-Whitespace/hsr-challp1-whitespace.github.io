---
layout: post
title: "Right-Left-Straight..."
date: 2015-10-11
categories:
author: "Roberto Cuervo & Stefan Kapferer"
---
## Sunday, 10. October 2015

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


{% endhighlight %}
And there we are with the three curves: blue are the row values, red are the moving average values and new, orange are the standard deviation values:
![Data Analyzer - standard deviation data](/media/data-analyzer_screenshot-02.jpg "Data Analyzer - standard deviation")

### First curve recognizer
The next step we took, was start trying to recognize curves ans straights. This first attempt used only the row data. We fixed a positive and negative threshold, and when the gyro z values are higher or lower, we have a right or a left curve, or a straight. 
This "silly" recognizer worked pretty good, but of course we could not trust it very much. The row values have peaks, and these invalid all the recognition. 

### Second curve recognizer
After exploring the track, we want to know where we are and how fast we can drive. Our approach is, first, split the track in curves or straights. We created a TrackPart class, and a enum:

{% highlight java %}

public enum Direction {
	RIGHT, LEFT, STRAIGHT

}
{% endhighlight %}

This "enhanced" curved recognizer uses moving averages. So we avoid peak values and use the nice red function in our graphs. 
The mechanism is again very simple: we read the values, and when they reach certain thresholds, we create a new instance of the TrackPart class in which we save the direction, start and end times. When the values reach another threshold, we create again the corresponding instance.

{% highlight java %}

public class TrackPart {
	
}
{% endhighlight %}


We save all these instances in a container class, because what we want is...

### Perodicity
Yes, we want to know when a new lap starts. In order to achieve that, starting from all the saved TrackPart instances we create a pattern like: RIGHT - LEFT - RIGHT -RIGHT - LEFT - STRAIGHT - LEFT
We compare continuously this pattern with the new ones incoming with each event, if we match, maybe we found the track model. If we found the model, maybe is time to start speeding up!!   



