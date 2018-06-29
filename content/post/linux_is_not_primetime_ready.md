---
title: "Linux Is Not Primetime Ready"
date: 2018-06-29T06:55:28+01:00
tags:
  - Linux
  - DistroD
categories:
  - Technical
draft: true
---

Browsing the [HackerNews thread](https:d//news.ycombinator.com/item?id=17413572) on a recent article criticising Apple keyboards, I was amused by a common discussion that always crops up on a subject like this: is Linux a viable alternative to Mac OS? To which the answer is always the same: no. But why is that?

<!--more-->

I'm writing this on Linux on my old Macbook Pro from 2011 so there's no doubt Linux can be an alternative desktop, even on Apple hardware. But that always comes with hefty caveats. I've been running Linux as my main OS for 6 years by now. I've learnt how to delve deep and resolve issues in many different parts of a Linux desktop system. Hell, I've written [my own distribution](https://github.com/sbreatnach/distrod)! Which I run on this Macbook, my home HP Z400 workstation and my work Thinkpad T450s. I've had problems at some stage with every one of those pieces of hardware.

As a rule of thumb, I upgrade my LTS every week to get latest security fixes and software updates. The problems I've had with Linux on these hardware configurations are (off the top of my head):

* Unable to boot on Thinkpad (initial Meltdown/Spectre fixes)
* Randomly unable to boot on Thinkpad (follow-up Meltdown/Spectre fixes)
* Unable to boot on Thinkpad (GRUB reconfiguration failure). This happened at least three times. 
* Unable to boot on Macbook (GRUB reconfiguration failure)
* Unable to upgrade Virtualbox (incompatible kernel header changes)

I could go on (there aren't any issues with the workstation cos I barely use it, btw). If I wasn't knowledgeable about Linux and software development in general, any one of these issues would've completely stymied me. The average person on the street, or even the average person working in a technical company, does not have this knowledge. For people like me, Linux is a viable alternative. Everybody else, you're stuck with MacOS and Windows. Sorry!