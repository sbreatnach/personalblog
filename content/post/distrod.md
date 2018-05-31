---
title: "My own Linux distro: DistroD"
date: 2018-05-31T07:34:28+01:00
tags:
  - Linux
  - DistroD
categories:
  - Technical
---

Linux is the best alternative if you're not running one of Windows or Mac OS, the two big juggernauts of the desktop OS world. There are a huge number of distributions that cover a range of use cases. But none really hit the sweet spot for me, so I built my own.

<!--more-->

Some form of Linux distribution has been my work OS for six years now. I experimented with Mac OS for a time before then but didn't like being tied to the Apple ecosystem and the limited, expensive hardware. Windows was the main before that but as I began to work more and more on server-side software, it made less and less sense. But Linux is not perfect, for one single reason: **instability**.

If you install one of the popular distros out there, such as Ubuntu, you get a modern interface and all the bells and whistles you'd ever need to use printers, external hard drives, etc. But all those features come at a price. Because Linux is primarily volunteer-driven, testing is never high on the list of priorities (testing is not fun!). Most of the projects out there have little to no automated tests and rely on users to do manual testing.

Which means, at any time, an update to your system can result in mystifying problems that weren't there before. Or maybe somebody thought it would be a good idea to remove a feature because "nobody was using it". I got tired of getting stung like this so I decided to build my own distribution: [DistroD](https://github.com/sbreatnach/distrod) (pronounced Distroed - yeah, I'm not good at names).

I'm still using off-the-shelf Linux components but, to remove the surface area for feature regressions and bugs, there are very few components and as low-level as possible. X server components or one level up was the goal. But I also wanted to support basic, useful things like automatic external drive mounting, easy application launching, keyboard layout switching, etc.

It's still very much a work in progress, but it's what I use for all my Linux installs now. At some point, I may make it a true distro with an integrated ISO install process. For now, it serves my purposes very well. And, bar one instance (goddamn you Virtualbox!), I've had no regressions in over a year of use.