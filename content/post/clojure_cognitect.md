---
title: "Clojure has a Cognitect problem"
date: 2018-10-25T06:12:34+01:00
tags:
  - Software
  - Clojure
  - Cognitect
  - Peopleware
categories:
  - Techical
---

I've been developing with Clojure full-time since 2015 and it's been a great experience overall. I've already posted about some of the features that really appeal to me but there are flaws too. Technical flaws, sure, but also organisational flaws. I was thinking about this due to a recent Twitter mini-controversy sparked by an episode of the [Apropos podcast](https://twitter.com/apropos_cast?lang=en).

<!--more-->

Stuart Halloway, one of the core developers of Clojure, was on this podcast. It was, on the whole, an interesting but largely innocuous conversation about various aspects of Clojure. But a few points that Stuart made raised the hackles of Zach Tellman, who is a well-known figure within the wider Clojure community. Crucially, he's not an employee of Cognitect or involved in the development of Clojure.

He made, as part of a series of tweets, the comment that ['"improving beginner experience" does not help the Clojure experts employed by Cognitect'](https://twitter.com/ztellman/status/1053127097667936256). This was in response to Stuart's comment that he's "resistant to arguments about improving beginner experience vs improving expert powers". 

When I listened to the podcast first, that assertion also made my eyebrows raise. That should never be an either/or proposition. It's perfectly possible to improve beginner experience while also offering more expert features. It's not easy, of course, but it should be doable. Now, perhaps he misspoke - it is all too easy to say something and have it construed differently to what you expected. The wider context was in comparison to Ruby On Rails, which is well known for having a superb beginner experience and yet being overly difficult when attempting complex customisations.

Ultimately, the podcast and the following Twitter comments will be forgotten and people will move on. But it does hark at a larger point: only Cognitect develops Clojure. Others can contribute and suggest but nobody except for Rich Hickey and employees of Cognitect have any real say in the language's direction. Up to now, that's not been a big problem. 

But then I see development of the [clj](https://clojure.org/guides/deps_and_cli) tool, which has a large amount of overlap with [Leiningen](https://leiningen.org/), the community's defacto build tool for Clojure. Leiningen, by the way, was not developed by Cognitect. And why was documentation on [clojure.org](https://clojure.org/index) so poor for so long? Could it be that the motivation wasn't there? The State of Clojure survey is an excellent way to engage the community, but it wasn't initiated by Cognitect. Instead it was another prominent figure in the Clojure community, [Chas Emerick](https://twitter.com/cemerick). The feedback from those surveys have only gradually affected the direction of Clojure with the number one complaint being finally addressed (inadequately, in my opinion) by [clojure.spec](https://clojure.org/about/spec).

I'm sure there are perfectly good explanations for all these. Nonetheless, to get back to the original point that Zach made, the driving force behind Clojure is Cognitect the company. While that is the case, there will always be a subliminal nudge to any choice made.

P.S. The [wikipedia page for Clojure](https://en.wikipedia.org/wiki/Clojure) says it's a community-driven project with a BDFL and barely makes a mention of Cognitect. Funny, that's not my impression.