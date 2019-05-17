---
layout: post
title: "When is it better not to write automated tests?"
categories: misc
---

The importance of writing and maintaining strong automated tests for software is well established in the modern software engineering community (and in fact, tests will be written before the code when using test-driven development, TDD).
But does it always pay off to write automated tests for some piece of code?
Are there situations where one is better off not writing automated tests?
Will you be considered to be a bad developer and chastised by your peers, users,stakeholders, or your manager if every line of code that you write is not under strong automated testing?

I have been wrestling with this question since 2007 when I first read the book "Working Effectively with Legacy Code" and radically changed my thinking about automated testing.
In the 10+ years prior to 2007, I wrote a lot of CSE software with very little strong automated testing.
I used the validation-centric approach [TriBITS Lifecycle Model] to test the software that I was writing.
As a result, I had personally written O(100k) lines of code that were being used others and was in the position to have to maintain.
When I realized that almost all of this software was considered "Legacy Code" according to "Working Effectively with Legacy Code" (i.e. "code without tests == legacy code"), I felt ashamed and horrified at mass of useful but buggy and difficult to maintain software that I had created and now myself and others would suffer due to this offense for years to come.  (Just recently a nasty bug in software I wrote in 2006 came up that caused a good deal of harm and was an embarrassment.)

After reading the book "Working Effectively with Legacy Code", I resolved to turn over a new leaf and become a born-again Agile software engineer that would use TDD to write all new code and religiously apply the Legacy Code Change Algorithm to modify all legacy code (i.e. code without tests).
Over the years since my conversion to an Agile software engineer, I often rigorously wrote automated tests for nearly every piece of software I touched.
There where times  under schedule pressure that I slipped (i.e. sinned) and reverted back to my old ways and failed to write good enough automated tests and came to regret it.
However, there were also times where my overzealous drive to religiously test everything (which usually came after the guilt of a recent slip of not testing enough) where I wasted time write automated tests that did not need to be written.
And now after having had followed this road from 2007 until now having written and maintained thousands of automated tests over that time, I have come to realize that there are times when it is actually better not to write automated tests for some pieces of software!

I have come to realize that it often does not pay off to write automated tests for a piece of software when the following five things are true about that software:

* **The damage done by a defect is minor.**
* **The majority of defects will be obvious.**
* **Fixing the majority of defects will be easy.**
* **Manually testing the software after a change is easy.**
* **Writing automated tests is hard or the tests will be hard to maintain.**

If all five of those criteria are satisfied, it is often better not to write automated tests for a piece of software.
The time spent writing, maintaining, and running the automated tests does not have enough benefit to outweigh the cost.

For example, a bash script used locally that loads some modules and then configures, builds, and runs tests for some software may not be worth testing because:

* The damage done by not having everything complete correctly will be minor because you can just run it again after it is fixed.
* A failure will be obvious because the software will not even build and no tests will be run.
* The script does pretty basic stuff and is easy to fix.
* It would be very difficult to write up mock objects to simulate the various shell commands in the script.

Therefore, it is often not worth the investment to write automated tests for locally run scripts of this type.

However, if such a script is being used to automate some important process like deploying the software to users and not performing the task correctly would cause non-trivial harm, you better write some automated tests to protect the critical functionality of the script.
Or, if other people are running the script it will not be obvious to them that a failure has occurred or they will not know how to fix it quickly, you better write some automated tests for the script.

For example, there was a bash test driver script in a CSE project where the script (run as a cron job) failed to detect that the code's tests were failing and instead sent out emails that everything was passing day after day.
As a result, the code was broken for weeks with no-one noticing.
A release of the software went out (to hundreds of internal users) and it was the users who noticed the new defects.
This wasted user's time, may have resulted in incorrect results, and damaged the reputation of the project.
The lesson is that some "scripts" may actually need to be considered software and need to have strong automated testing just like any piece of software.  (Just become some piece of software is written in bash or python does not mean it can be dismissed as "scripts" and avoid any automated testing.)

Note that if the first four criteria above are true but it is not too hard to write automated tests, then often one should write them anyway because it will make the code easier write and to maintain going forward.

Also note that adjectives like "minor", "obvious", "easy", and "hard" are all subjective and do not have precise definitions.
For example, something that seems "minor", "obvious", "easy" and/or "hard" for one person, another person may consider "major", "non-obvious", "difficult", and/or "easy".
For example, if one does not know the sensing, separation, and fake collaborators strategies for unit testing described in "Working Effectively with Legacy Code", then one might think that adding automated tests for a piece of software is "hard" while another more skilled/knowledgeable/experienced developer might consider adding tests for that piece of software to be quite tractable.

*Disclaimer:* Therefore, please don't use this blog article as an excuse for not writing automated tests for some piece of software by trying to convince yourself that the damage of defects will be "minor", any failures will be "obvious", or the defects will be "easy" for anyone to fix.
You might think that but your users, stakeholders, and other developers (who will need to maintain this software) may not feel the same way.
