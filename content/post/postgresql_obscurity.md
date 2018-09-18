---
title: "Mailing List Obscurity: Postgresql"
date: 2018-09-06T06:13:16+01:00
tags:
 - Postgresql
 - Mailing Lists
categories:
 - Technical
---

One of the methods of communication over the internet that software developers favour are mailing lists. I don't know much about the history of mailing lists but they pre-date forums, Q&A sites like Quora or StackOverflow, blogs, comment threads, and most of the many other ways that people talk to each other via the World Wide Web.

They also annoy the hell out of me. I was reminded of this yesterday when investigating an issue with Postgresql.

<!--more-->

There are many obvious problems with mailing lists:

* **Noisy** - any mailing list view page shows tons of useless information, such as email message IDs, email addresses, random characters as part of replies, etc.
* **Repetition** - information is repeated over and over, which must be filtered out by the suffering reader. For example, if viewing an index page for a mailing list, the subject for a busy email thread is shown repeatedly.
* **Difficult to parse** - when skimming mailing lists for some solution, it's extremely difficult to discern the wheat from the chaff. The noise and repetition feeds into this, but it's also related to the mailing list viewers out there. Most don't do any form of syntax highlighting or visual break up of the wall of text.
* **Not searchable** - most (all?) search engines mark down mailing list entries, mainly because of the aforementioned problems. When searching for an obscure issue, you are more likely to get a tutorial by some random blogger instead of insight from one of the main developers of the program.

Most of these problems are inherited from email and they're not going away any time soon. Collectively, the whole of humanity appears to have accepted email's failings and moved on.

Which brings me to the issue I found with Postgresql. I have been making use of [foreign data wrappers](https://wiki.postgresql.org/wiki/Foreign_data_wrappers) at work, a nice little feature which allows me to seamlessly "import" a table from one database to another. Well, not that seamless.

According to [an obscure mailing list entry](https://www.postgresql.org/message-id/26654.1380145647%40sss.pgh.pa.us) which took me hours to find, there is no way to safely insert a new row into a foreign table that uses a serial column. The sequence that populates the unique values of the serial column must be local to the foreign table, which is clearly not workable when there is already a sequence in the foreign database. There is [no official documentation](https://www.postgresql.org/docs/9.4/static/postgres-fdw.html) on this at all, bar this mailing list entry. This wouldn't be so much of a problem if a standard search found this entry quickly. But it doesn't - it took at least 10 different variants on my keywords across two different search engines before it cropped up as the fifth result.

Now, you could argue this is a failing of the Postgresql developers in this case and not necessarily the mailing list format. This deficiency should be officially documented. But, in my experience, developers who use mailing lists are more likely to make this mistake. They see these emails come in daily and subconciously assume that everybody else gets the same visibility. But those emails, once archived, are almost invisible to your average Joe Searcher for the reasons above.

What's the answer? The easy one is to **stop using mailing lists!** Many solutions have been developed in the decades since their use began that are an improvement. But I guarantee that a significant number of those developers would fight tooth and nail to retain their mailing list sanctum, despite the obvious flaws. Alternatively, developing better mailing list archive software that better surfaces these lists without the noise. But that's a fundamental problem with email and nobody has worked that one out yet as far as I know.