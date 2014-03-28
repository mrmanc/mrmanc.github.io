---
layout: post
title: Bad Interpreter—SVN autoprops save the day
cover: bad-interpreter.jpg
categories:
- Bash
- UNIX
- Windows
- Shell
- SVN
- Subversion
published: true
---

A number of times I’ve had to fix problems with shell scripts which have been edited or created on a Windows system and committed with Windows CRLF line endings, then checked out on to a UNIX system and executed. Perhaps you’ve seen this output somewhere?

    /bin/sh: filename.sh: /bin/bash^M: bad interpreter: No such file or directory  

Another common one is scripts which are not marked as executable, meaning that they can’t be run whenever then end up where they’re meant to be.

This is very easy to fix on a case by case basis by running `svn propset svn:eol-style "native" filename.sh` and `svn propset svn:executable "*" filename.sh`. The first tells Subversion to translate line endings to suit the system you are on—LF on UNIX and CRLF on Windows. The second tells it then when it is on UNIX systems it should set the executable permission for users, groups and others.

However, I have a terrible memory so I forget to recite such incantations. A better idea is to configure your subversion client to do this automatically. You can enable auto-props by editing `%USERPROFILE%\Application Data\Subversion\config` on Windows or `~/.subversion/config` on UNIX systems. You want to make sure that you have an uncommented line saying `enable-auto-props = yes` and further down in the file extensions section a line saying `*.sh = svn:eol-style=native;svn:executable`. From memory it doesn’t ship with a configured eol-style of native so you’ll have to change that (or leave it as LF if you’re not feeling kind towards Windows users—they’ll struggle to edit the file in some editors).

There—job done. Now you can forget about fiddling with properties until you move to a new system. Of course you might want to take this setting with you—perhaps you need a [dotfiles project](2014-03-25-bash-dotfiles-bindle.html) (yes I know I haven’t put it in there… yet)?
