---
author: markisadeveloper
comments: true
date: 2011-07-30 21:20:13+00:00
layout: post
slug: automating-vuze-with-dropbox-in-os-x
title: Automating Vuze with Dropbox (in OS X)
wordpress_id: 19
categories:
- Life Hacks
tags:
- Applescript
- Azureus
- Bittorrent
- Dropbox
- Mac
- OSX
- Vuze
---
This is a simple one, but I’m quite pleased with it, and I don’t think it jumps out as an obvious tweak. Fuze (formally Azureus) is a great BitTorrent client, which has some great features like transcoding and subscriptions. I’ve previously had it configured to download everything from an RSS feed, which was built from my bookmarks in Mininova. But they don’t have so many torrents these days, and I wanted a set up which wasn’t dependent on one site.

Anyway. Vuze allows you to configure a watched folder, from which it loads any torrent files added. You can configure this to be any folder, so you just need to pick one in your Dropbox.

[![Vuze Torrent Watched Folder](http://markisadeveloper.files.wordpress.com/2011/07/screen-shot-2011-07-31-at-17-15-45.png)](http://markisadeveloper.files.wordpress.com/2011/07/screen-shot-2011-07-31-at-17-15-45.png)

The slightly less obvious thing is that if you have Dropbox installed on your iPhone / iPad, then you can download files within Safari and choose to place them in your Dropbox from that device. So as long as you have Vuze open, you can kick off a download just by downloading the torrent file from your mobile device.

If you’re like me though, you probably close Vuze when it’s not doing anything. So for bonus points, why not set up some AppleScript to open Vuze when a file is added to your folder? I’ve not used AppleScript before, except to hook some stuff up with Automator. But it’s actually really easy to configure a script for your folder, and it only needs to be three lines long to fire up Vuze. I’ve included it below for reference. Save it to "/Library/Scripts/Folder Action Scripts/" (you’ll need to sudo copy it there). Just right click the folder, and choose Folder Actions, and choose your script.

{% highlight applescript %}
on adding folder items to this_folder after receiving added_items
try
tell _application_ "Vuze"
activate
end tell
end try
end adding folder items to
{% endhighlight %}

Test it out, and hey presto, you’re done!
