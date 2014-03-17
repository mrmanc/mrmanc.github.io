---
layout: post
title: Free hosting with Github Pages
cover: GitHub_Logo.png
date:   2014-03-16 21:58:00
categories: posts
status: publish
---



I’ve made the move from Wordpress to [Jekyll](http://jekyllrb.com/), and Wordpress.com for hosting, to [Github Pages](http://pages.github.com/) which has Jekyll support built in. Combined with Github Pages (which is an awesome way to host HTML sites for free), this is a very powerful way to get an easy to manage blog with complete control and no sales pitch for extras.

In short, Jekyll gives you a framework to write your posts in [MarkDown](http://daringfireball.net/projects/markdown/), and easily compile them to HTML by running a simple command.

Combined with Github Pages (which is an awesome way to host HTML sites for free), this is a very powerful way to get an easy to manage blog with complete control and no sales pitch for extras.

You just have to write your post in a MarkDown file, run a Jekyll command and then commit / sync your change to the GitHub repository. You even get optimisation of JS, CSS and images thrown in for free.

I first followed [this simple Wordpress migration guide](http://hadihariri.com/2013/12/24/migrating-from-wordpress-to-jekyll/) to move my posts, and hacked an [existing Jekyll theme](http://the-development.github.io/flex/) to fit my purposes. That migration mechanism left me with HTML files instead of MarkDown. I then used [exitwp](https://github.com/thomasf/exitwp) which was much more successful, but required a little review. There are lots of other migration guides on the [Jekyll Import site](http://import.jekyllrb.com/docs/home/).

I wish I’d seen [Octopress](http://octopress.org/) before I got started—I’ll move to that when I get a chance.

Using your own domain is as simple as creating a file with it in in the repository, and changing the DNS to point at Github.

Get started by reading [this simple Github guide](http://pages.github.com/).
