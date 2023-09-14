---
title: "So long FreeBSD"
date: 2023-09-14T06:27:31+01:00
tags:
  - FreeBSD
  - Linux
  - DistroD
  - Nostalgia
categories:
  - Technical
---

Considering my career since, it's surprising to think that the first \*nix-like OS I used in anger was not some flavour of Linux. Instead it was **FreeBSD**. As such, I've always had a fondness for it despite the fact I haven't actually used it since. So when I was looking for a little project to pass the time, I thought "Why not port [DistroD](https://github.com/sbreatnach/distrod) to FreeBSD?" That's when reality finally met my rose-tinted glasses.

<!--more-->

After Upstart Games collapsed, I still wanted to use my 4 years experience working with mobile phones. And that's what happened, for a year, with a company called Bluemetrix. But once that project stalled, they found me something else to do within the company: working on the web UI for their core web analytics system. And the OS they ran their entire backend on? FreeBSD.

Once I left Bluemetrix in 2010 to become a contractor, I never came across FreeBSD in a work environment again. Linux was already taking over and if Linux wasn't being used, it was Windows. But I always had a hankering for returning to FreeBSD.

How did the port of DistroD go? The basics were there on the hardware of my Thinkpad T480s: suspend and resume was functional, sound worked no problem, the webcam was usable and the HiDpi display scaled identically to the equivalent Linux install. Unfortunately, the fit and polish was poor out of the box. Some of it was trivial and fixable, but some fundamental issues remained:

- A couple of "stable" ports were broken and the (trivial) fixes were only in the current snapshot.
- Since Widevine DRM has not been ported to FreeBSD and never will be, you can't stream any legit music, TV or movies.
- Despite some sterling community efforts using jails, there is no equivalent to Docker.

The first problem was worrisome because it suggested that there wasn't enough manpower to backport fixes to the stable branches.

As for the last two problems, what is the solution? Running a Linux emulation layer or using a Linux VM. This is the crux of the problem. **Why should I persist with FreeBSD when I can install Linux and not have these problems?**

Frankly, FreeBSD gives me nothing over Linux.

It used to be the case that [FreeBSD's documentation](https://docs.freebsd.org/en/books/handbook/) was superior. This is not true any longer. I came across multiple errors and omissions while investigating and resolving the various issues I had, some trivial and some not. More problems were resolved using [the Arch Linux wiki](https://wiki.archlinux.org/) than the FreeBSD handbook.

FreeBSD's general performance used to be the equal or better of Linux. No longer; boot times were slower and general speed differences so negligible as to be unnoticeable.

Perhaps there are some other aspects I am unaware of but, for my day-to-day usage, the FreeBSD experience was seriously deficient.

---

It's a shame. I used to love FreeBSD. But it is gradually becoming a victim of the slow consolidation of OS platforms that's been happening since the 90s. Windows is for the average user, macOS is for the well-off average user and Linux is for everybody else. There's no room for FreeBSD and, without any hard numbers to go on, there's a sense that their community is shrinking and will eventually fade away.

I'm contributing to that consolidation but, like so many things in life, you have to pick your fights. 👋
