---
layout: post
title: "Project Kickoff"
date: 2015-09-21
categories:
author: "Stefan Kapferer"
---
## Monday, 21. September 2015, *Project Kickoff*
Today we had the project kickoff of our Challenge Project.
Wolfgang Giersche from [zühlke](http://www.zuehlke.ch) introduced us to the challenge.
See the presentation slides [here](/media/challenge_teaser.pdf).

### The Challenge
Implement an autopilot for 'carrera' track:

![Carrera track](/media/carrera.png "Carrera track")

The algorithm should analyse the track and then learn
how to drive with maximal possible speed.

### Technology
The [Starter-Kit](https://github.com/FastAndFurious/AkkaStarterKit) is implemented with [Java](http://java.com/) and [Akka](http://akka.io/), therefore we will also use these technologies.

### Links
We should study/google the following buzzwords for better understanding of the project,
if we dont already know them:

 - real time event processing
 - maching learning
 - microservices
 - internet of things
 - reactive programming
 - data analytics
 - [Spring Framework](http://spring.io/)
 - [Akka](http://akka.io/)

### First steps
The first 'little' (more or less) step today was to get
the starter-kit running on our machines.

The requirements:

 - maven
 - jdk8
 - rabbitmq-server

Basically the starter-kit can be cloned from [https://github.com/FastAndFurious/AkkaStarterKit](https://github.com/FastAndFurious/AkkaStarterKit) and then built with *mvn clean install*. (snapshots of 'fnf.clientapi' and 'fnf.simulib' in local maven repo is required)
After overcoming some barriers with the simulator-gui, it worked.

**Reminder / TODO:**
Some points are not very nice, I think we have to improve these things.
For example I dont want to checkout some dependencies and build local snapshots
to make a project running. Such dependencies should be binary.
Unfortunately there is no release with the current sources in the repository.
I think we will setup our own CI (Jenkins) and artifact repository.

In the end we set up our github repositories and finished the day.

### Summary
The project sounds very exciting but also very challenging.
Maybe thats why it is called 'challenge' project. :D
There are a lot of interesting concepts and technologies we do not know yet.

This will be a lot of work, I think... I hope we will also have some fun with it :-)

