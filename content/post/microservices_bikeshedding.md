---
title: "Microservices Bike-shedding"
date: 2018-07-13T06:14:28+01:00
tags:
  - Microservices
  - Service-Oriented Architecture
  - Software Engineering
categories:
  - Technical
---

A common approach to architecting a platform in the software industry is [microservices](https://martinfowler.com/articles/microservices.html). There appear to be fundamental issues with it though. Every now and again, [somebody writes an article](https://segment.com/blog/goodbye-microservices/) about their bad experiences with it and [online forums respond](https://news.ycombinator.com/item?id=17499137), loudly declaring they're doing it wrong. Is it any wonder though, when it's so poorly understood?

<!--more-->

The microservices link is the first article that comes back from Google when you search microservices: a large article from Martin Fowler's website describing microservices. It describes a near-utopian vision of decentralised development, each service completely independent from the other, owned by a development team and communicating via HTTP or message queues.

I am being deliberately reductive here because the article is very comprehensive and goes into detail about all aspects of the architecture. But most people don't really read the article, or don't fully understand the nuances, which leads to the afore-mentioned bad experiences. I speak from experience because I've made these mistakes myself and (hopefully) learned from them.

Instead of drilling down into every aspect of my learnings, let's use the most powerful tool in documentation: bulletpoints! Here's a short list of do's and don'ts I recommend:

* DO split your services by clearly-defined and obvious domains
* DON'T split your services prematurely
* DO use an event-based architecture
* DON'T use microservices with a small team - 50+ developers at a minimum
* DO document your service APIs
* DON'T use microservices without good devops/sysadmin knowledge in the team
* DO build robust retry mechanisms into every service boundary

It's a fascinating topic because microservice architecture is a very powerful paradigm but all too easily misused. I'll do some more posts on some of my experiences because there's plenty to talk about.