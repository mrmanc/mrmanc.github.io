---
layout: post
title: Saving the world, one dashboard at a time
comments: true
image: dashing.jpg
date: 2013-05-22 13:05:46+00:00
---

A colleague asked us recently to make sure we turn our monitors off overnight to save power. That’s all very well, but what should we do about our dashboard? We purposefully disable power saving to make sure that the display doesn’t turn off during the day, and since we never actually use it there would be nothing to wake it up! It turns out you can easily script this using Task Scheduler, which comes with Windows. You will need to download a tool called [NirCmd](http://www.nirsoft.net/utils/nircmd.html), which allows you to control your monitor from the command line (amongst many other things). You already have a command called powercfg to configure the other Power Saving options from the command line.

[![dashboard-monitors](http://markisadeveloper.files.wordpress.com/2013/05/dashboard-monitors.jpg?w=300)](http://markisadeveloper.files.wordpress.com/2013/05/dashboard-monitors.jpg)

Simply create a scheduled task that runs at, say 8am, which runs the following two actions:
`powercfg -x monitor-timeout-ac 1
C:\nircmd-x64\nircmd.exe monitor off`

and one for 7pm that runs:
`powercfg -x monitor-timeout-ac 0
C:\nircmd-x64\nircmd.exe monitor on`

Make sure you put the proper path you’ve unzipped NirCmd to. You could do without the monitor timeout being changed, but if the mouse get’s nudged during quiet time, the monitor won’t turn off again.

We specifically turn the monitor on in the morning after disabling the power saving option, as there is no mouse or keyboard activity to prompt it to wake - otherwise the team will just be looking at a blank screen all day.
