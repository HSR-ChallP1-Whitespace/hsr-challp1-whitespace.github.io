---
layout: post
title: "First improvements after our 'real world' experiences"
date: 2015-11-16
categories:
author: "Roberto Cuervo, Stefan Kapferer"
---
## Monday, 16. November 2015

### Introduction
This Lab-Log entry is a summary of all we did after our training-day. (06.11.)
We worked on the following days:

 - sunday, 08.11.2015
 - sunday, 15.11.2015
 - monday, 16.11.2015

### Track recognition without round times
The first thing we did, was the redesign of our track recognition logic. We used the round time, which isn't usable on the real track. 

The idea to solve that: When we matched the pattern after the second round, we just drive another (third) round to check if the pattern is correct. 
We implemented a new solution:

 - for each pattern we match, we create a new actor
 - the actor checks if he can confirm the pattern
 - if the pattern can be confirmed (pattern repeated again), the actor sends a message to the main track recognition actor to tell him that the pattern is correct
 - the sub-actor stops working and the main actor starts the position detector on the confirmed pattern

### Use less constants in our algorithm
We used a lot of time to discuss how we can reduce our constants/thresholds. There are some which are easier to calculate and others which are difficult.
The main problem was the threshold of the standard deviation of the GYR-Z, which we use to detect the straight parts.
We discussed a lot of solutions how we maybe can detect the straight parts without the standard deviation. But how? If we could detect the noise in the straight parts, that could be a solution. 
But still we don't have an idea how to detect the noise without using a variance or standard deviation :-/

We have to think about this point again. We didn't implemented any improvements till now.

### Failure tolerance in track recognition
Another problem is the failure tolerance of our track recognition logic. If we don't match the pattern after first two rounds, the logic will never find anything. 
The most times we don't match the track it's just because of a small failure in the pattern. For example because we have a small straight part in one round which we don't have in the other.
Our first idea: Maybe we could improve the PatternMatcher, so that we check how big the failure is. If the patterns only differ in one part, we could create two actors which try to confirm both of them.

We implemented a first experimental solution now, which also tries to confirm patterns with a small failure. We used a 'levenshtein distance' algorithm to calculate the failure. 
After a few tests we saw that this solution has it's problems till now, but we are on a good way. 

We have to improve that solution and get a logic which retries if it doesn't worked.

Thats all for now.
