---
layout: post
title: "When is it better not to write automated tests?"
categories: misc
---

## Introduction

The importance of writing and maintaining strong automated tests for software is well established in the modern software engineering community (and in fact, tests will be written before the code when using test-driven development, TDD).
But does it always pay off to write automated tests for some piece of code?
Are there situations where one is better off not writing automated tests?
Will you be considered to be a bad developer and chastised by your peers, users, stakeholders, or your manager if every line of code that you write is not under strong automated testing?

I have been wrestling with this question since 2007 when I first read the book "Working Effectively with Legacy Code"<sup>[1]</sup> and radically changed my thinking about automated testing.
In the 10+ years of my professional career prior to 2007, I wrote a lot of Computational Science and Engineering (CSE) and applied math software with very little strong automated testing.
I used the validation-centric approach<sup>[2]</sup> to test the software that I was writing.
As a result, I had personally written O(100k) lines of code that were being used by other people and was in the position to have to maintain.
When I realized that almost all of this software was considered "Legacy Code" according to "Working Effectively with Legacy Code" (i.e. "code without tests == legacy code"), I felt ashamed and horrified at the mass of useful but buggy and difficult to maintain software that I had created and now myself and others would have to deal with for years to come.
(Just recently a nasty bug came up in software I wrote around 2006 without strong automated testing that caused a good deal of harm and was an embarrassment.)

After reading the book "Working Effectively with Legacy Code", I resolved to turn over a new leaf and become a born-again Agile software engineer that would use TDD to write all new code and religiously apply the Legacy Code Change Algorithm to modify all legacy code (i.e. code without tests).
Over the years since my conversion to an Agile software engineer, I often rigorously wrote automated tests for nearly every piece of software I touched.
There where times  under schedule pressure that I slipped and reverted back to my old ways and failed to write sufficient automated tests and came to regret it.
However, there were also times where my overzealous drive to religiously test everything (which usually came after the guilt of a recent slip of not testing enough) where I wasted time writing automated tests that were not worth the effort.
And now after having had followed this road from 2007 until now having written and maintained thousands of automated tests over that time, I have come to realize that there are times when it is actually better not to write automated tests for some pieces of software!

## Criteria for when it is better to not add automated tests

I have come to realize that it often does not pay off to write automated tests for a piece of software when the following five things are true about that software:

* **The damage done by a defect is minor.**
* **The majority of defects will be obvious.**
* **Fixing the majority of defects will be easy.**
* **Manually testing the software after a change is easy.**
* **Writing automated tests is hard or the tests will be hard to maintain.**

If all five of the above criteria are satisfied, it is often better not to write automated tests for a piece of software.
The time spent writing, maintaining, and running the automated tests does not have enough benefit to outweigh the cost.

For example, some bash scripts used locally that load some modules and then configure, build, and run tests for some software may not be worth writing an automated test suite for because:

* The damage done by not having everything complete correctly will be minor because you can just run it again.
* A failure will be obvious because the software will not even build and no tests will be run.
* The scripts do pretty basic stuff and will be easy to fix if they fail.
* It would be difficult to write mock up the various commands run by the script.

Therefore, it is often not worth the investment to write automated tests for locally run scripts of this type.

## Example where automated tests should have been added

However, if such scripts are being used to automate some important process like deploying the software to users where not performing the task correctly would cause non-trivial harm, then one should write some automated tests to protect the critical functionality of the scripts.
Or, if other people are running the scripts and it will not be obvious to them that a failure has occurred or they will not know how to fix it quickly, then one should likely write some automated tests for the scripts.

For example, there was a bash test-driver script in a CSE project where the script (run as a cron job) failed to detect that the code's tests were failing and instead sent out emails that everything was passing.
As a result, the code was broken for weeks with no one noticing.
A release of the software went out (to hundreds of internal users) and it was the users who noticed the new defects.
This wasted user's time, may have resulted in incorrect results, and damaged the reputation of the project releasing the software.
The lesson is that some "scripts" may actually need to be considered *software* in their own right and need to have strong automated testing just like any piece of non-trivial software.
(Just become some piece of software is written in bash or python does not mean it can be dismissed as "scripts" and avoid any automated testing.)

## Notes

Note that if the first four criteria above are satisfied but it is not too hard to write automated tests, then often one should write them anyway because it will make the code easier extend and to maintain going forward.

Also note that adjectives like "minor", "obvious", "easy", and "hard" are all subjective and do not have precise definitions.
For example, while for one person might consider these five criteria as "minor", "obvious", "easy", "easy" and "hard", another person may consider them "significant", "non-obvious", "not easy", "painful", and/or "tractable".
For example, if one does not know the sensing, separation, and fake collaborators strategies for unit testing described in "Working Effectively with Legacy Code", then one might think that adding automated tests for a piece of software is "hard" while another more skilled, knowledgeable, and/or experienced developer might consider adding tests for that piece of software to be quite tractable.

## Summary

While it often pays of to write a high quality automated test suite for a piece of software (i.e. reduce initial development costs and improve long-term maintenance), there are situations where it does not pay off.  Here we listed five criteria that if satisfied, it is better not to write automated tests and instead do manual testing when any changes are made to the code.

## Disclaimer

Please don't use this blog article as an excuse for not writing automated tests for some piece of software by trying to convince yourself that the damage of defects will be "minor", any failures will be "obvious", or the defects will be "easy" for anyone to fix.
You might think that but your users, stakeholders, and other developers (who will need to maintain this software) may not feel the same way.
So please use discretion when applying this criteria to some piece of software when deciding whether or not to write automated tests (and how much testing is reasonable).

<br>

[1]: #ref1 "Feathers, Micheal C. Working Effectively with Legacy Code.  Prentice Hall, 2004, ISBN: 0131177052"
[2]: #ref2 "Overview of the TriBITS lifecycle model: A Lean/Agile software lifecycle model for research-based computational science and engineering software."

<br>


References | &nbsp;
:--- | :---
<a name="ref1"></a>1 | [Feathers, Micheal C. Working Effectively with Legacy Code.  Prentice Hall, 2004, ISBN: 0131177052](https://www.oreilly.com/library/view/working-effectively-with/0131177052/)
<a name="ref2"></a>1 | [Bartlett, Roscoe A., Micheal A. Heroux, James M. Willenbring. *Overview of the TriBITS lifecycle model: A Lean/Agile software lifecycle model for research-based computational science and engineering software.*  IEEE 8th International Conference on E-Science, 2012](https://doi.org/10.1109/eScience.2012.6404448)

<br>



