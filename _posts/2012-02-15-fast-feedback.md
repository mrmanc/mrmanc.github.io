---
author: markisadeveloper
comments: true
date: 2012-02-15 22:55:52+00:00
layout: post
slug: fast-feedback
cover: fast.jpg
title: Fast Feedback
wordpress_id: 55
categories:
- Agile
- Development
tags:
- ant fast build
- Checkstyle
- continuous integration
- JUnit
- PMD
- software-development
---

My relationship with Ant has had its ups and downs. I hate writing a build file in a language that I'm unfamiliar with, and finding that the language seems designed to encourage and hideous result. Recently however I felt I achieved something, successfully reducing the duration of our teams pre check in task task from three and a half minutes to only 24 seconds.

I think this is important that number of reasons. The first is that we are aiming to check in more often. The closer to your last check in you are, the easier and cheaper it is to use revert to recover from wrong turns. If the target takes too long, it becomes a barrier to checking in and tempts you to do just a little more.

Secondly, as many developers will attest, the longer you spend staring at Ant output the more context leaks out of your brain, until you find yourself just staring blankly into space. It doesn't help with the natural cadence of development.

Finally, time is money! Three minutes ten times a day across a large team can amount to hundreds of pounds worth of wasted time.

So what does our target do? Well, in it's fifth incarnation it runs a cut down set of unit tests, and checks we haven't introduced any measurable code quality issues using PMD and Checkstyle. In the past it has done anything we could think of:

* run our unit tests
* run our integration tests
* run our http container tests with the app running in Jetty
* run our selenium browser tests
* run our jstestdriver JavaScript tests
* instrumented our classes using Cobertura and guarded against drops in test coverage
* PMD and Checkstyle checks as mentioned above

It has evolved over time depending on how frustrated we were with it's length, and what we were working on at the time (hence what the risks were). At our lowest, we were spending around fifteen minutes running tests before checking in.

It was suggested to us that we should be able to hold our breath whilst our tests run, and I'm glad to say that even the smokers of the team should be able to do that for 24 seconds.

Whilst pragmatically sacrificing coverage has got us so far, the recent drop required something a bit more sophisticated. Two techniques have helped: running tests in parallel and only quality scanning modified files out of sync with Subversion.

The first part is achievable due to the experimental [ParallelComputer](http://kentbeck.github.com/junit/javadoc/latest/org/junit/experimental/ParallelComputer.html) class introduced into JUnit. You can write a test suite which uses the class to run several tests in parallel programmatically. There are draw backs - the cost of the parallelisation may in fact increase the time your tests take. It took ours from 50 seconds to 12. Also, when the suite is invoked from Ant we've been unable to get it to generate the usual JUnit XML results - only the one test (our suite) gets reported. Still, hopefully the class will mature into either a test runner or option in the JUnit Ant task.

The second was a lucky guess that paid off - the SVNAnt library happens to provide a number of built in file selectors - my favourite being [svnmodified](http://subclipse.tigris.org/svnant/selectors.html#svnmodified). This allows you to create filesets containing only those files you have edited since your last check in. I've used this to restrict our PMD and Checkstyle operations and the effect was awesome. PMD was the biggest culprit spending ages longer than the tests themselves. PMD now runs in just six seconds!

Is it finished? No, of course not - it can always get faster, and unchecked will always gradually get slower. As we work on different aspects of the applicant we will find it more important to run different types of tests. And as we mature the types of tests we depend on will change. We could probably be smarter about what we clean and compile, perhaps even which tests we run.

So next time you find yourself staring at a screen full of any gibberish, think about reducing the amount of work your build does by being creative.

Image credit: [Rocket Man](http://www.flickr.com/photos/peasap/2261077597/)
