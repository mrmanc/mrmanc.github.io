---
layout: post
title: Take your scripts with you
categories:
- Bash
- OS X
- Mac
- UNIX
- Shell
- Dotfiles
- Command line
- Configuration
cover: china-country-postman.jpg
---

I often feel quite nomadic when using Bash. I’m somewhat a hobo developer, moving from home to home. Recently I’ve been working with OS X at work, and I’ve been on OS X at home for years. Yet still I had some machines where my bash history would drop off quickly, and where aliases I use a lot didn’t exist. When I worked out how to get hostname completion working with ssh I decided it was time to have a dotfiles project.

In case you’re not familiar with the concept of a dotfiles project, the term dot file refers to settings files whose filename typically starts with a dot in UNIX. For example, there’s your `.bash_profile` file which indicates what should be run when you login. You may have Git settings defined in `.gitconfig`. A dotfiles project is one which lets users synchronise their dotfiles across different machines.

Before starting my own, I had a look at some of the projects that already exist, indexed on [GitHub does dotfiles](http://dotfiles.github.io/). A popular project is [Oh-My-Zsh](http://ohmyz.sh/), which may suit you if you use Zsh as your shell. As a homeless developer I have to use what I find, so I wanted to stick with Bash. Zach Holman has an [interesting project](http://zachholman.com/2010/08/dotfiles-are-meant-to-be-forked/) with some ideas I really liked. But I didn’t find anything for Bash that I really liked.

I had been surprised that the installation of some dotfiles projects does a lot more than installing some dotfiles, doing things like changing Mac settings etc. This is my Bash bindle—not my OS X bindle—so I didn’t want that.

I wanted the project:

- To not ‘install’ anything
- To be very easily added to using filename conventions to allow the elements of customisation to be found rather than specified
- To be entirely self contained other than a single hook into the user’s profile
- To be removed as easily as removing a single line and removing the directory
- To be easily extended by adding a single directory, potentially outside the bindle
- To be ignorant of whether you are on a Mac
- To play nicely with existing profiles and configuration

### Bash Dotfiles Bindle

<blockquote cite="http://en.wikipedia.org/wiki/Bindle">
A bindle is the bag, sack, or carrying device stereotypically used by the commonly American sub-culture of hobos.
</blockquote>
[Bindle](http://en.wikipedia.org/wiki/Bindle), from Wikipedia

With these preferences in mind, I created [Bash Dotfiles Bindle](https://github.com/mrmanc/bash-dotfiles-bindle) on Github, and I think it fits all the above requirements. There’s not much in it yet, but now that I have a means to synchronise my settings I’m spending more time finding the ‘right’ way to do things, and to save those things in the bindle so that I can use them elsewhere later. Running the installation installs a hook into `.bashrc` (the interactive non-login profile), which sets up the environment. If it looks like there is no call from `.bash_profile` (the interactive login profile) to also run `.bashrc` then it adds one. If you don’t understand the difference between the various profile files, [this answer](http://stackoverflow.com/questions/415403/whats-the-difference-between-bashrc-bash-profile-and-environment#answer-415444) explains it perfectly.

There’s no commitment by installing it, and it gives you [some cool stuff](https://github.com/mrmanc/bash-dotfiles-bindle#features) by default.

[Go get it and start building a better home.](https://github.com/mrmanc/bash-dotfiles-bindle)
