---
author: mark
layout: post
title: Test Driven Development in Bash
cover: tests-passed.png
categories:
- Bash
- UNIX
- Shell
- Testing
published: true
---

I’ve found myself wanting the convenience of some Bash unit testing for the third time, and not wanting to develop yet another set of assertion functions I thought it was about time to find something reusable. I’m looking to do the basic asserts, with some regular expression matching and a sprinkling of [self shunt](http://c2.com/cgi/wiki?SelfShuntPattern) (with command interactions intercepted by replacing commands like echo with functions within the scope of the test). I should credit [Ross Beazley](https://twitter.com/be4zley/) for starting me off on this approach. This time I’m resisting the temptation to start a new project and thought I’d find something to fork and improve. So here are a few of the projects I found and a bit of analysis.

Desirable features

* Regular Expression pattern matching
* Summary of results
* Breakdown of which tests passed/failed
* Ability to show results of all assertions in a test (not just the first that failed)
* Discovery of test definitions by filename
* Color

## ShUnit
[Docs](http://shunit.sourceforge.net/), [Sourceforge](http://www.sourceforge.net/projects/shunit)
Last updated Dec 2012
Downloaded 376 times in the last year

Whilst I like the summary that this tool gives you, I don’t really like the output as it doesn’t describe failures. Also frankly I’ve struggled to work out what sort of assertions are supported, or how to use it quickly.

    *************** shUnitTest ****************
    10 tests to run:
    ...
    ================================================
        Test 9: TestOneAssertFailureAndOneAssertSuccessMeanFailure
    ------------------------------------------------
    Assertation Results: E..
    ================================================
          "This test failed intentionally" failed.
    ================================================
        Test 10: TestOneDenyFailureAndOneDenySuccessMeanFailure
    ------------------------------------------------
    Assertation Results: E..
    ================================================
          "This test failed intentionally" failed.
    ================================================
    Results of Suite:
    --------------------------------------------------

    10 tests run.
      10 tests succeeded.
      No tests failed.

    ================================================

## shUnit2
[Docs](http://shunit2.googlecode.com/svn/trunk/source/2.1/doc/shunit2.html), [Github](https://github.com/zanshine/shunit2), [Google Code](https://code.google.com/p/shunit2)
101 stars on Google Code.
Last updated May 2011

This one looks okay. It roughly equates JUnit and works on a number of platforms (OS X and Cygwin included) and a number of shells (sh, bash, zsh etc). It appears to have been developed by one person and hasn’t been developed since May 2011, but I’m guessing that’s because it’s feature complete for it’s intended purpose.

The following assertions are supported. That just leaves me missing regex support.

* assertEquals [message] expected actual
* assertNotEquals [message] expected actual
* assertSame [message] expected actual
* assertNotSame [message] unexpected actual
* assertNull [message] value
* assertNotNull [message] value
* assertTrue

The output is a bit thin

    testEquality
    testPartyLikeItIs1999
    ASSERT:It's not 1999 :-( expected:<1999> but was:<2014>

    Ran 2 tests.

    FAILED (failures=1)


## Conclusion

I’m going to have a go at extending shUnit2 to support regular expressions. More soon!
