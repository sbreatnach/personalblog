---
title: "Nostalgia: Japanese Game Porting"
date: 2018-06-11T06:51:44+01:00
tags:
  - Nostalgia
  - J2ME
  - Programming
categories:
  - Technical
---

A recent post about finding the keyboard shortcut for [debug mode in Animal Crossing](https://jamchamb.github.io/2018/06/09/animal-crossing-developer-mode.html) (via [Hacker News](https://news.ycombinator.com/item?id=17277157)) had my nostalgia senses tingling. It reminded me strongly of my first job: porting Japanese mobile phone games to European handsets.

<!--more-->

### Upstart Games

Upstart Games was my first job out of university, where I still held hopes of working in the computer game industry. It was the closest I came to this goal before I was turned off by the crazy stories filtering back to me via the interwebs (e.g. [EA spouse](https://ea-spouse.livejournal.com/274.html)).

Upstart wasn't like the fancy-dan companies doing "real" games, like EA, Ubisoft, et al. We had business connections to a number of Japanese game companies and, for a one-off fee, we took the original codebase used with Japanese phones and ported them to European phones. Japan had a booming mobile game industry at the time (2004 approximately) based on some superb mobile phones that were years ahead of the dross in Europe. Remember, this predates the iPhone by some margin; Nokia and Motorola were the dominant brands and they were, for gaming at least, atrocious software platforms.

One of the companies we dealt with was [Konami](https://en.wikipedia.org/wiki/Konami). We ported a number of their best-known franchises: Dance Dance Revolution, Contra, Gradius, etc. But the one that sticks in my mind most was Castlevania. Most of the porting of Castlevania and the various versions we got from Konami was handled by me. There were basically three versions: a stripped down version that was very close to the original NES game, a slightly more upgraded version that made heavy use of the VSCL 1.1 custom API, and a QVGA, VSCL 2.0 version.

### API Shenanigans

[J2ME](https://en.wikipedia.org/wiki/Java_Platform,_Micro_Edition) was the common platform used. Sun had managed to persuade all these mobile phone companies to embed a stripped-down Java Virtual Machine (JVM) into every phone, no matter how limited the hardware was. The original Japanese codebases were J2ME technically also, but they used a lot of custom APIs that were specified by the phone carriers, such as VSCL. In some cases, there were no replacement APIs on the European devices. For example, MIDP 1.0 was the baseline for most phones but this had no API for playing sound of any sort. Something of an issue for games...

(While fruitlessly looking for links on the VSCL API, I came across [this gem](https://web.archive.org/web/20180611052224/http://www.bus.umich.edu/kresgepublic/journals/gartner/research/116800/116858/116858.pdf). It's funny to read it now. Imagine, Vodafone thought they knew how to guide the market via a closed, curated platform (!). This mentality would persist until 2010ish when the success of the iPhone became apparent to even the dumbest executive.)

### Porting Castlevania

Why was I reminded of this by a random article about debug mode in a Gamecube game? Because I had to do similar investigations with the original codebases. Konami developed these codebases using their own in-house platform. It attempted to combine the support of all the various J2ME API flavours into one codebase using the power of C preprocessors. This also meant engineers used macros and #defines for actual code. This had the added bonus of supporting tricks to reduce code size, a major issue back then with 30KB limits on Java JAR files the standard.

Did we get access to this in-house platform? Nope, of course not! Instead, we got the compiled version of the code with the macros and #defines already processed. It had no comments of any sort and highly useful variable names like `a`, `aa` and `h`. You would have to work with code like the following:

{{< highlight java >}}
	case 3:
		h[10] = 3000;
		h[11]  = 0;
		h[9] = 0;
		h[13] = -1;	
		h[14] = 0;
		h[8] = 0;
		h[12] = 5;
		h[15] = 64;

		ob[0][0] = 1;
		ob[0][1] = 1;
		ob[0][2] = 0;
		ob[0][11] = 0;
		ob[0][12] = 64;
{{< / highlight >}}

For the most part, this sort of code could be ignored because it was game logic and could be left untouched. But if there was a bug in the original logic, or it needed to be tweaked because of some specific device issue? Oh boy.

I learnt a lot working with these codebases. I may do some follow-up posts about them because, looking back, they are fascinating.