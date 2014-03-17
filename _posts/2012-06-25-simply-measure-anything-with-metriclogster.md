---
author: markisadeveloper
comments: true
date: 2012-06-25 22:56:06+00:00
layout: post
cover: ruler.jpg
slug: simply-measure-anything-with-metriclogster
title: Simply Measure Anything with MetricLogster
wordpress_id: 121
tags:
- graphite
- Logs
- logster
- MetricLogster
- metrics
- Monitoring
- Visualisation
---

Okay, so my [previous post](http://markisadeveloper.wordpress.com/2012/05/10/meet-graphite/) is a long overdue summary of how we are visualising application metrics using Graphite. We are writing custom Logster parsers which scan our log files and push interesting things into Graphite. This means that to get a new metric into Graphite we need to add it to our log files (unless it already exists), and adapt or create a python Logster parser to understand whatever we've logged. This parser then needs to be deployed to our server running logster and a graph built. The biggest blocker we've seen with this approach is the necessity for the engineer to understand how to write Python, where to find and test the Logster parsers, and how to deploy the parser to the Logster server. Personally, this means either doing the work myself or explaining the peculiarities of Python white space handling to yet another person. There must be a better way.

It has occured to us to use StatsD to simplify this stuff by the way, but we're not convinced it is designed to scale.

A couple of months ago I had the idea of creating a generalised parser to make this process easier. A little Googling discovered that, as usual, someone had already had a similar idea. Jeff Blaine had [committed](https://github.com/jblaine/logster/commit/a6a1da5a3a1ad527f3493cfe4b561893932207ec) a MetricParser (as detailed in this [blog post](http://www.kickflop.net/blog/2012/03/30/any-metric-graphing-with-graphite-and-syslog/)) which was intended to be used with syslog. This dealt with the use case of wanting to log counter type metrics, however we also find ourselves logging a lot of time based metrics which don't lend themselves to being totalled up as a counter.

So in discussion with Jeff I have rewritten the MetricLogster to accept time based metrics, and modified the format slightly.

The upshot of this is that once you've got MetricLogster hitting your application's log files, then creating a new metric in Graphite is as simple as creating a line of log, for example (using Log4J):


    logger.info("METRIC_COUNT name=customer.checkout value=1");


Or, if you are logging a time, you can just do:


    logger.info("METRIC_TIME name=request_duration value=150ms");


Once you've got your application writing those statements, the MetricLogster parser will pick them up and understand what to push to Graphite. In the case of counts, you are only really interested in the total figure - how many customers checked out, how often a service failed etc. When you are logging times however it makes no sense to total them up; you want to know what some aggregate function returns for the set of times. Usually, you're interested in the mean, median (if you've realised that the mean doesn't tell you much), and possibly something like the interquartile range to tell you how distributed the values were.

So, what do you get for free? For the above, you would get:

* customer.checkout (as a total)
* request_duration.mean
* request_duration.median
* request_duration.90th_percentile

This is the purpose behind stating in the log file what sort of metric it is. Configuring what percentiles to record is just a matter of specifying them as parameters in the call to Logster.

But wait: this doesn't just work for Log4J! If you can adapt your log format, you can use this for anything! All you have to do is conform to the syntax and the parser will do the rest. And Jeff's idea of hooking this up to your syslog server is very smart - that way rather than having to wire up the parser and your log file each time you build a new app, you can just hook up one syslog server (or even a cluster) and get all the benefit of UDP fire and forget integration with your Graphite server, via a UDP > Syslog > log file > Logster > Graphite route.

I'm still waiting for my pull request to get processed, So in the meantime:

**[look here for the new MetricLogster](https://github.com/mrmanc/logster/blob/master/parsers/MetricLogster.py)**

(and you'll need [stats_helper](https://github.com/mrmanc/logster/blob/master/parsers/stats_helper.py))

Set it up, tell people about it and see what happens.

One line change == metrics in Graphite == win!
