---
layout: post
title: Meet Graphite
comments: true
categories:
- Agile
- Development
- Performance
- Visualisation
tags:
- code as craft
- etsy
- graphite
- graphs
- logster
- measure
- metrics
- stats
date: 2012-05-10 23:58:10+00:00
---

Last year i was fascinated by a [presentation](http://velocityconf.com/velocity2011/public/schedule/detail/17776) [[slides]](http://www.slideshare.net/mikebrittain/metrics-driven-engineering-at-etsy) by Etsy about their approach of metrics driven engineering - see their blog post - [Measure Anything, Measure Everything](http://codeascraft.etsy.com/2011/02/15/measure-anything-measure-everything/). They started with some questions: how many of us had access to our production logs (a reassuringly high amount), and how many of us could tell them how many hits our application was getting right now / how many hits it got this time last year.

They outlined how they use [Graphite](http://graphite.wikidot.com/) to visualise how their applications are running in their live environment, and how they use [logster](https://github.com/etsy/logster) and [StatsD](https://github.com/etsy/statsd) to feed information in from a variety of sources such as log files and UDP packets sent by their application. The metrics shown in Graphite are an aggregate view of things like response codes, response time, checkouts and basically any other arbitrary information their engineers find interesting. Their mantra of measure everything stems from the fact that this is valuable data, which can [quickly indicate issues with deployments](http://codeascraft.etsy.com/2010/12/08/track-every-release/) (they deploy around 20 times a day) or the environment the application runs in.

The confidence that this gives them allows them to move faster and respond more quickly. So, should they deploy a fresh new build and see the HTTP 5xx status codes jump, or the checkouts suddenly dip, they can respond by reverting ASAP. Having access to this sort of real time data is incredibly powerful (not to mention addictive).

The advice is to make it easy for developers to get metrics into Graphite, and then sit back and see what happens. So the two main feeder technologies you have to work with are:

* **StatsD** - a node.js app which collates metrics from UDP packets and performs some aggregation
* **Logster** - a Python framework which allows you to adapt or create parsers easily which aggregate information from your log files

#### Screenshots

So, I’ll show you some pretty pictures. Graphite is a web application which provides a view on to aggregated data. It provides the ability to build custom charts with the metrics you have pushed in using Logster, StatsD or something else. You can further aggregate data series and use [other functions](http://graphite.readthedocs.org/en/1.0/functions.html) to transform the data you are interested in. You can view metrics over arbitrary time periods and drill down to as much granularity as you’ve recorded (most likely the individual server level if you used Logster).

![](http://graphite.wikidot.com/local--files/screen-shots/graphite_fullscreen_800.png)

It also has a dashboard builder, albeit slightly lacking - we have built custom dashboards using the simple image api - configuration, functions and metric names are passed by parameter in a simple URL.


![](http://graphite.wikidot.com/local--files/screen-shots/graphite_cli_800.png)

#### Our progress

Almost one year on and we have a number of teams in the organisation feeding data into Graphite using logster. We have data coming from browsers, from Apache, from applications through Log4J, from Squid and more. Interest is still growing but we have already seen huge benefits and an improvement to our stability response.

[![](http://markisadeveloper.files.wordpress.com/2012/05/dashboard.png)](http://markisadeveloper.files.wordpress.com/2012/05/dashboard.png)Dashboards mounted on walls keep us up to date with problems and have become the heartbeat for our applications. When we are deploying we watch for issues closely, and we keep a weather eye on the app all day. Although we’re not quite at the point where we’re controlling our own deployments, our delivery team have taken a lot more responsibility for the application’s stability, which can only be a good thing.

So what sort of things do we log? In the chart below you can see our traffic pattern over a 48 hour period, with a 24 hour offset level in green for comparison. Although this is a fairly static chart it does sometimes alert us to serious stability issues when our traffic has dropped steadily, and once to a DNS misconfiguration which sent a high volume of traffic for another application to ours.

[![](http://markisadeveloper.files.wordpress.com/2012/05/traffic.png)](http://markisadeveloper.files.wordpress.com/2012/05/traffic.png)

More changeable is a chart of error indicators such as log statements above WARN, and HTTP 500 status codes issued to users. This is one of the most telling chart of them all, indicating anything from a faulty external dependency to some sort of scraping activity.

[![](http://markisadeveloper.files.wordpress.com/2012/05/errors.png)](http://markisadeveloper.files.wordpress.com/2012/05/errors.png)

We also show a chart of the median response times for requests, and a measure of the realistic time it takes users to load pages, as reported by browsers using the [Boomerang](http://yahoo.github.com/boomerang/doc/) library. As well as reassurring us of the shape of our overall page performance, it allows us to see when our users are impacted by slowdowns caused by database issues, slow external dependencies etc.

From an obscure black box a year ago to a realistic view of our application’s innards today, we’ve come a long way.


#### What’s next?


_**Alerting**_; since this information is valuable to us we intend to improve our response by hooking up something like [Graphite Tattle](https://github.com/wayfair/Graphite-Tattle) or [Nagios](http://www.nagios.org/) to provide us with alerts when metrics exceed thresholds. Further, using the [Holt Winters functions](http://graphite.readthedocs.org/en/1.0/functions.html#graphite.render.functions.holtWintersAberration) recently introduced in Graphite we intend to make these alerts smart, basing their confidence of an event on previous data.

_**Aggregation**_; using Logster we have a view of metrics split between application servers, since that is the granularity of our log files. Ideally we would like to record some metrics over multiple servers. This can be done with StatsD, but due to concerns and uncertainty over scalability and redundancy we are considering alternatives.

_**Dashboards**_; alternative front ends to Graphite are available such as [Graphiti](https://github.com/paperlesspost/graphiti), and we plan to evaluate these to see if they fit our needs better than our custom efforts.

_**Easy creation of metrics**_; I am about to contribute a generalised Logster parser to the project which will make the creation of useful metrics as easy as adding one line of debug, following a prescribed syntax. This should make it trivial for developers to count interesting events in the application such as exceptions or user activities.
