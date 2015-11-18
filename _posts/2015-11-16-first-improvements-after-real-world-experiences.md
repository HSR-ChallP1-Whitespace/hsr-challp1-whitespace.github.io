---
layout: post
title: "First improvements after our 'real world' experiences"
date: 2015-11-16
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Monday, 16. November 2015

### Introduction
This Lab-Log entry is a summary of what we did after our training-day. (06.11.15)
We worked on the following days:

 - sunday, 08.11.2015
 - sunday, 15.11.2015
 - monday, 16.11.2015

### Track recognition without round times
The first thing we did, was the redesign of our track recognition logic. We used the round time, which isn't usable on the real track. 

The idea to solve this: after matching the pattern in the second round, we just drive another (third) round to check if the pattern is correct. 
We implemented a new solution:

 - for each pattern we match, we create a new actor
 - the actor checks if he can confirm the pattern
 - if the pattern can be confirmed (pattern repeated again), the actor sends a message to the main track recognition actor to tell him that the pattern is correct
 - the sub-actor stops working and the main actor starts the position detector on the confirmed pattern

### Use less constants in our algorithm
We used a lot of time to discuss how we can reduce our constants/thresholds. There are some which are easier to calculate and others which are difficult.
The main problem was the threshold of the standard deviation of the GYR-Z, which we use to detect the straight parts.
We discussed a lot of solutions about how we could detect the straight parts without the standard deviation. But how? If we could detect the noise in the straight parts, that could be a solution. 
But still we don't have an idea how to detect the noise without using a variance or standard deviation :-/

We have to think about this point again. We didn't implemented any improvements till now.

### Failure tolerance in track recognition
Another problem is the failure tolerance of our track recognition logic. If we don't match the pattern after first two rounds, the logic will never find anything. 
The most times we didn't match the track were just because of a small error in the pattern. For example: we had a small straight part in one round which we didn't have in the other.
Our first idea: Maybe we could improve the PatternMatcher, so that we can check how big is the error. If the patterns only differ in one part, we could create two actors which would try to confirm both of them.

We implemented a first experimental solution, which tries to confirm patterns with a small error. We used a 'levenshtein distance' algorithm to calculate this error (error = distance in levenshtein's algorithm). 
After a few tests we saw that this solution has its problems too, but we are on a good way. 

We have to improve this solution and get a logic which retries if it doesn't work.

Thats all for now.
