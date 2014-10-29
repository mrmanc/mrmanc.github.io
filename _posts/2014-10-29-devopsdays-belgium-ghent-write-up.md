---
layout: post
title: DevOpsDays Ghent, Belgium 2014
cover: ghent-market-hall.jpg
comments: true
categories:
- devops
- devopsdays
- conference
- belgium
- ghent
---
I’ve just made it back from DevOpsDays in Ghent, Belgium. This was my first DevOpsDays event, and the atmosphere was celebratory as it was the fifth anniversary of the first, and sadly Patrick Dubois’s last event as the main organiser as he is stepping down.

Thanks go to Patrick and the rest of the organisers who had gone to incredible lengths to look after the attendees, including shuttle buses from the hotel, a generous breakfast both days and even an fantastic evening meal on the Monday. This meant that we could make the most out of meeting people and discussing each other’s experiences.

Also, Ghent is one of the prettiest cities I have ever seen.

## Devops

There was some retrospecting on the last five years of the devops movement, and plenty of discussion around the culture surrounding the area. From the developer biased turnouts at local events I was surprised to find myself very much in a minority as someone whose origins are in development. There was discussion around whether we are all developers now, which I felt were inevitable as the terms ops and dev are in the title of the event. It feels to me that it is much more useful to describe people’s responsibilities as engineering rather than focussing on ops and dev as separate roles, particularly as doing otherwise undervalues the years of experience that many people have in each area.

As highlighted by Gareth Rushgrove in [issue 1 of DevOpsWeekly](https://github.com/garethr/devopsweekly/blob/master/_posts/2010-11-30-issue-1.textile), “It’s safe to say Devops means different things to different people”, and that led to a few inevitable meta discussions about the meaning of the term. Speaking time was split between organised speakers and an open session format, with a fun ignite segment in between to wake us up after lunch. I was surprised at people were more focussed on culture than on technology, but in retrospect this makes sense with a conference which is centered around a subject variously understood to mean collaboration and respect.

<blockquote class="twitter-tweet" lang="en"><p>Nothing on this slide has changed since 2010 except the &quot;at this early stage&quot;. <a href="https://twitter.com/garethr">@garethr</a> <a href="https://twitter.com/hashtag/devopsdays?src=hash">#devopsdays</a> <a href="http://t.co/8ovyfhoiMN">pic.twitter.com/8ovyfhoiMN</a></p>&mdash; Bridget Kromhout (@bridgetkromhout) <a href="https://twitter.com/bridgetkromhout/status/527097774433902592">October 28, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

## Open Sessions

The open sessions were a great opportunity to get a grass roots view of what is going on in the companies the attendees came from. It was fascinating to find that no one was running Docker (at least at any scale), despite the conference’s ‘Docker… Docker… Docker’ meme highlighting the excitement around the technology. Similarly no one was able to say they are using immutable infrastructure in their organisations. Deployable images were mentioned a number of times, although this was conflated with immutable infrastructure.

#### Repository management

I was surprised and pleased to learn that plenty of people want to improve their Linux repository management, making server builds deterministic whilst still updating packages from upstream repositories. [@mini_inny](https://twitter.com/mini_inny/with_replies) mentioned [aptly](http://www.aptly.info/) as a versioned package repository for Debian, but it does not support RPMs ([yet](https://github.com/smira/aptly/issues/39)). Thinking beyond OS packages, and more around products, [Ringo De Smet](https://twitter.com/ringods) talked about his product in development [ReleaseQueue](http://www.releasequeue.com/), which promises to allow you to version the collection of packages, recipes, gems, jars, wars and whatever else your product needs to run (the ‘bill of materials’), providing private URLs where appropriate for repository clients (such as apt-get). This is a very smart approach, since it is the product that we care about, and I look forward to seeing whether it would suit us.

I was pleased to have caught the session about Ops Learning (especially with regard to development practices) and will be exploring some of the ideas such as pull requests for operations code review, fun side projects such as implementing something specific in a new language, reading other people’s pull requests and Ops focussed hack days.

Logging was a well attended session, with many people using and advocating [Elasticsearch / Logstash / Kibana](http://www.elasticsearch.org/overview/), some using Graphite and StatsD, and some using [Reimann](http://aphyr.github.io/riemann/) for alerting and statistical modelling.

## Presentations

Tuesday’s talk about “[The Cognitive Neuroscience of Empathy](http://www.slideshare.net/dmangot/the-cognitve-neuroscience-of-empathy-youre-a-devops-natural)” was excellent, and a fascinating insight into how we are hard wired to exhibit empathy with our peers through mirror neurons. The conclusions that you should praise more, trust more and treat others as *you* expect to be treated seem like excellent goals.

<blockquote class="twitter-tweet" lang="en"><p>Slides (with notes) from my <a href="https://twitter.com/hashtag/devopsdays?src=hash">#devopsdays</a> Ghent presentation &quot;The Cognitive Neuroscience of Empathy&quot; <a href="http://t.co/Xi0tSimWXI">http://t.co/Xi0tSimWXI</a></p>&mdash; Dave Mangot (@davemangot) <a href="https://twitter.com/davemangot/status/527120569498882048">October 28, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

I also took quite a bit away from Brian Troutwine’s talk about “[Automation with Humans in Mind](http://www.slideshare.net/BrianTroutwine1/automation-with-humans-in-mind-making-complex-systems-predictable-reliable-and-humane)”, (see the [article on InfoQ](http://www.infoq.com/news/2014/10/devops-days-automation-humans) for a wordier summary) particularly about what good automation looks like, and how it is important to understand what you are building—abstraction is necessary but you shouldn’t be ignorant (sentiments echoed the evening before in hotel bar discussions).

<blockquote class="twitter-tweet" lang="en"><p>I&#39;ve put my <a href="https://twitter.com/hashtag/devopsdays?src=hash">#devopsdays</a> slides online! <a href="http://t.co/rkUp7rU5ZC">http://t.co/rkUp7rU5ZC</a> Thanks everyone for for listening; it was a delight! &lt;3</p>&mdash; Brian L. Troutwine (@bltroutwine) <a href="https://twitter.com/bltroutwine/status/527089083169140736">October 28, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

I think one of my favourite things though has to be introducing a [BuzzFeed employee](https://twitter.com/damianigreg) to [What if programmers used BuzzFeed-style commit messages](https://storify.com/anirvan/buzzfeed-style-commit-messages).
