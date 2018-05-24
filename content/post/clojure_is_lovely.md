---
title: "Clojure Is Lovely"
date: 2018-05-24T21:16:06+01:00
tags:
  - Programming
  - Clojure
categories:
  - Technical
---

In my current job, I've been using Clojure as one of the main languages. Every time I go back to it, it makes my heart soar. Ok, I might be overexaggerating a little. But it is great.

<!--more-->

The functional style makes it easy to create code that is clean and concise. Check this out:

{{< highlight clojure >}}
(into {} (for [[uid timestamp] uid-timestamps
                :let [configs (get uid-configs uid)]]
           [uid {:timestamp timestamp :configs configs}]))
{{< / highlight >}}

Three lines that are easy to read. It takes a map of unique IDs to timestamps (`uid-timestamps`) and constructs a new map of unique IDs to a map containing a timestamp and configuration data for the unique ID. Nothing particularly special about what the code does, but see **how** it's done.

First off, Clojure's native **data structures are immutable**. There is no method of updating the map in-place. This feature instantly removes a whole host of potential bugs; I don't have to think about side-effects to the original map, and the injected configuration will not change after this code has finished. 

Secondly, **the basic set of syntax is tiny**. Clojure has additional syntax for Java interoperability, macros and other advanced features. It also has syntax that act as sugar to reduce code and improve clarity. But that code snippet contains everything required to write a Clojure program. For example, a map is usually declared like `{:timestamp timestamp}` but this is just syntactic sugar for `(hash-map (keyword timestamp) timestamp)`.

Thirdly, **nil punning**. What happens if `uid` is null? Or if `uid-configs` is null? In most languages, this would be a hard crash - NoneType, NullPointerException, pick your poison. In Clojure, it will happily keep on going. So, if you invoke `(get nil nil)`, it will simply return nil. Which, if you think about it, makes sense. I first came across this type of behaviour in Objective-C and I was delighted when I found Clojure did it too. 

Not everybody feels the way I do about nil punning and I do see their point of view. Sometimes, you don't want code to continue because it hides the immediate bug and could result in a bug elsewhere in your code. It would then make it harder to track back to where the nil first crept in. But, in my experience, getting annoying NullPointerExceptions or having to constantly put in guard expressions and branches to handle nulls is the far greater frustration.

All these features can be difficult to grok if you are used to imperative languages because you have to take entirely different approaches to problems you've solved many times before. But once it becomes second-nature, you will wish this sort of elegance existed in all languages.