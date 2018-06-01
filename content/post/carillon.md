---
title: "Simple Linux keyboard switching: Carillon"
date: 2018-06-01T09:22:58+01:00
tags:
  - Carillon
  - Keyboards
  - Linux
categories:
  - Technical
---

As part of my work on my custom Linux distribution, I needed an application that:

* had a graphical user interface,
* listed a set of keyboard layouts,
* applied them when changed,
* used low-level X components only.

A very simple set of requirements. And yet, I couldn't find anything. Most of them are tied to a specific desktop environment, like GNOME or KDE. Or they use their own complex components, like iBus. I knew about xkb but everything I'd used was either CLI-only or were static graphical views.

So I built my own: [Carillon](https://github.com/sbreatnach/carillon) (which is a form of musical keyboard and is a nicely unique name). As a version 1, it's functional but basic. It works with a fixed set of keyboard layouts from a YAML file, which can be put in a number of locations. There's a simple systray icon that supports selecting the layout manually. That's it!

I will revisit it at some stage because I did it in Python initially. This made it easy to build up a quick prototype, but as a long-term approach it's inefficient and difficult to distribute due to Python dependencies. The interface is what I want though. It fills a basic need for [my custom distro DistroD](https://github.com/sbreatnach/distrod) which I [blogged about before]({{< relref "post/distrod.md" >}}). Maybe Rust, or Swift?
