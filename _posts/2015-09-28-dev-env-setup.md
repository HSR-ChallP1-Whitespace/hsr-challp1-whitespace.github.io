---
layout: post
title: "Dev environment setup"
date: 2015-09-28
categories:
author: "Stefan Kapferer"
---
## Monday, 28. September 2015, *Dev-Env setup day*

### DEV-Env
Today we used a lot of time to setup our projects and development environment. The starter-kit has two dependent
projects which need to be build locally. (snapshots) Otherwise the starter-kit-project will not build. I do not like
this setup. The project should build with a *git clone ...* and *mvn clean install*. 

For this reason we forked those projects and created our own artifact repositories were we can deploy releases.
We also created Jenkins-Jobs to continuously build our projects. Snapshots are automatically deployed to the
SNAPSHOT-Repository after each commit and successful build. To create RELEASES, we start the job manually.

### autopilot-project
Based on the starter-kit we created our own [autopilot-project](https://github.com/HSR-ChallP1-Whitespace/autopilot).

### environment documentation
All the links and the documentation of the development environment can be found [here](/dev-env).
