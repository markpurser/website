---
layout: post
title: "Hierarchical statecharts"
author: Mark Purser
date: 2016-11-12 12:39:23 +0000
comments: true
categories: [Software Architecture, Defender, Hierarchical Statechart, Partitioning, Coupling, Cohesion]
published: false
---

This is the first article in what I plan to be a series loosely based around software partitioning.

Seeing as I like retro games I decided to use Defender as an interesting model to base my study. I will be exploring architectures for the game using hierarchical statecharts<a href="#1"><sup>1</sup></a>, factoring and functional decomposition. The principles should scale up to larger systems.

This is very much a practical working through of issues and essentially a 'brain dump' of different ideas. As much as you can read the countless articles and books on the subject nothing beats working through the issues yourself.

I'm motivated by making better decisions at the architectural level and thus producing better quality software.

{% img /images/hierarchical_statecharts/Defender_Statechart-2.png Defender Top Level Statechart%}
Figure 1 - Defender Top Level Statechart

The system is partitioned at the top level by decomposition into orthogonal<a href="#1"><sup>1</sup></a> sub-components, those that are independent and concurrent.

{% img /images/hierarchical_statecharts/player-spaceship.png Player Spaceship%}
Figure 2 - Player Spaceship

{% img /images/hierarchical_statecharts/human.png Astronaut%}
Figure 3 - Astronaut

{% img /images/hierarchical_statecharts/invader.png Invader%}
Figure 4 - Invader

{% img /images/hierarchical_statecharts/projectile.png Projectile%}
Figure 5 - Projectile

NB. I have left out entry and exit functions for clarity.

<h3>Remarks</h3>

The advantage of the startchart is the clarity of the diagrams. They communicate your intent, at least for simple examples such as this.

But how do we go about implementing this design? It comes down to creating a dispatcher and sending events around the system. See Miro Samek's implementation<a href="#2"><sup>2</sup></a>

A problem is how do you get information from the invader to the game-world for display? It needs to be sent as an event. The partitioning into local state means that you can't data share. The resolution is events.

Join me next time for more architectural fun.

This *is* a [reference link][id] example

If you want advice please <sup>call</sup> me. If I cannot help I will point you to someone who can.

BCS code of conduct

This is [an example](http://example.com/ "Title") inline link.

<h3>References</h3>

<sup id="1">1</sup> David Harel, Statecharts: A visual formalism for complex systems.
<br>
<sup id="2">2</sup> Miro Samek, Practical Statecharts in C/C++, CMP Books 2002.



[id]: http://example.com "Optional title"