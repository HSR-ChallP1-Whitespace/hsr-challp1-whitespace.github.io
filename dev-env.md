---
layout: page
title: dev-env
permalink: /dev-env/
---
## Endpoints
**[Source code repositories](https://github.com/HSR-ChallP1-Whitespace/):**

| Repo          | Link                                                                                                                                                     |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autopilot     | [https://github.com/HSR-ChallP1-Whitespace/autopilot](https://github.com/HSR-ChallP1-Whitespace/autopilot)                                               |
| clientapi     | [https://github.com/HSR-ChallP1-Whitespace/fnf.clientapi](https://github.com/HSR-ChallP1-Whitespace/fnf.clientapi)                                       |
| simulib       | [https://github.com/HSR-ChallP1-Whitespace/fnf.simulib](https://github.com/HSR-ChallP1-Whitespace/fnf.simulib)                                           |
| Lab-LOG ([page](http://hsr-challp1-whitespace.github.io/)) | [https://github.com/HSR-ChallP1-Whitespace/hsr-challp1-whitespace.github.io](https://github.com/HSR-ChallP1-Whitespace/hsr-challp1-whitespace.github.io) |


**[Nexus artifact repositories](http://nexus.kapfi.ch):**

| Repo          | Link                                                                                                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| snapshots     | [http://nexus.kapfi.ch/nexus/content/repositories/challp1-fastandfurious-snapshots/](http://nexus.kapfi.ch/nexus/content/repositories/challp1-fastandfurious-snapshots/) |
| releases      | [http://nexus.kapfi.ch/nexus/content/repositories/challp1-fastandfurious-releases/](http://nexus.kapfi.ch/nexus/content/repositories/challp1-fastandfurious-releases/)   |

**[CI - Jenkins Jobs](http://jenkins.kapfi.ch):**

| Repo          | Link                                                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------------------------------------ |
| autopilot     | [http://jenkins.kapfi.ch/jenkins/job/hsr-challp1-autopilot/](http://jenkins.kapfi.ch/jenkins/job/hsr-challp1-autopilot/) |
| clientlib     | [http://jenkins.kapfi.ch/jenkins/job/hsr-challp1-clientlib/](http://jenkins.kapfi.ch/jenkins/job/hsr-challp1-clientlib/) |
| simulib       | [http://jenkins.kapfi.ch/jenkins/job/hsr-challp1-simulib/](http://jenkins.kapfi.ch/jenkins/job/hsr-challp1-simulib/)     |

## Build autopilot
{% highlight bash %}
git clone git@github.com:HSR-ChallP1-Whitespace/autopilot.git
mvn clean install
# Maybe its necessary to:
cd autopilot/src/main/resources/public
bower install
{% endhighlight %}

## Run autopilot
{% highlight bash %}
java -jar target/autopilot-{version}.jar 
{% endhighlight %}
... and open simulator in browser under [http://localhost:8089/](http://localhost:8089/).

## requirements to build and run
 - mvn
 - jdk8
 - rabbitmq-server 
