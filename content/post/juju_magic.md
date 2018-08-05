---
title: "Juju Black Magic"
date: 2018-07-26T21:09:16+01:00
tags:
  - Juju
  - DevOps
  - LXD
categories:
 - Technical
---

As part of my general readings, I came across an interesting tool called [Juju](https://jujucharms.com). It's developed by Canonical and my best attempt at describing is that it is a **macro-infrastructure provisioning tool**. But my initial experience was poor because their tutorial simply didn't work out of the box.

<!--more-->

Juju is designed to quickly build up a large-scale deployment, such as a Hadoop or Kubernetes cluster. It also supports scaling the deployment after the fact with some simple commands. It's a nice idea for sure.

Testing it out is supported with [LXD](https://linuxcontainers.org/lxd/), a Linux service that works with LXC containers and is comparable to it's far more popular cousin, [Docker](https://www.docker.com). The downside of using LXD is that the community is far smaller and common problems not well documented.

I tried following the local cloud tutorial in the Juju docs and hit a number of roadblocks. As illustration of how inaccurate the tutorial is, this is the verbatim command history from my shell:

    sudo snap install juju
    sudo snap install lxd
    /snap/bin/lxd init
    /snap/bin/lxc network edit lxdbr0
    >> config:
    >>   ipv6.address: none
    >>   ipv6.nat: "false"
    sudo ufw disable
    /snap/bin/juju bootstrap localhost lxd-test

A few points of explanation:

* Note the use of /snap/bin as a prefix otherwise your shell won't find the binaries by default. Unless you run them as sudo, but this can lead to it's own issues.
* The default bridge LXD generates adds IPv6 support, but this is not supported by Juju and the bootstrap immediately errors unless you disable IPv6.
* The local firewall had to be disabled because Juju's controller is blocked from accessing the host LXD API otherwise. I haven't determined the precise rule needed to enable this because there is 0 documentation around the controller requirements (in the tutorial at least). UPDATE: it seems like only port 8443 needs to be opened.

I got there eventually, but I very nearly gave up a number of times. Only the promise of what Juju offers kept me going. Plus, my personal motto is ["Never give up, never surrender"](https://www.youtube.com/watch?v=SJ2hJezvd2I).
