---
layout: post
title: Static Analysis of Shell Scripts
cover: shellcheck.png
comments: true
categories:
- shell
- scripting
- UNIX
- bash
- quality
- devops
---
Static analysis has been a widely used tool in development teams for some time now. So when I saw this tweet about [ShellCheck](https://github.com/koalaman/shellcheck) I was very interested. I’ve looked for some wisdom about shell scripting best practices in the past, and not found much useful. Plus, [automating your coding standards](http://programmer.97things.oreilly.com/wiki/index.php/Automate_Your_Coding_Standard) being one of the [97 Things Every Programmer Should Know](https://www.google.co.uk/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0CC8QFjAA&url=http%3A%2F%2Fwww.amazon.co.uk%2FThings-Every-Programmer-Should-Know%2Fdp%2F0596809484&ei=X3s9U_7YHrGV7Abns4DYDQ&usg=AFQjCNF6I5nBRCYnyAiIdatoviQRoeuWCA&sig2=U6wPuwGjIjF0xNQZXstVTw), perhaps a tool like this is much more valuable.

<blockquote class="twitter-tweet" lang="en"><p>Seriously, if you write shell/bash, and want it not to suck, you should use some of this <a href="https://t.co/nKfTRWqHMA">https://t.co/nKfTRWqHMA</a> if you don’t, lucky you!</p>&mdash; Ben Hughes (@benjammingh) <a href="https://twitter.com/benjammingh/statuses/451506083128152064">April 2, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

I use OS X so I am lucky enough to be able to install it locally. The [installation instructions](https://github.com/koalaman/shellcheck#building-with-cabal) don’t mention Windows (although they do cover Debian & Fedora), so I’m gonna guess you’ll struggle to get it working under something like Cygwin. In any case, there is an awesome UI on <http://www.shellcheck.net/> which will give you feedback on scripts you have pasted in, with [clickable links](https://github.com/koalaman/shellcheck/wiki/SC2086) to wiki pages explaining any wisdom which doesn’t seem obvious to you.

# OS X Installation

If you are using OS X you can install using (mostly) brew, but I ran into a few difficulties so I thought I’d include them here, in case I forget to contribute to the documentation.

These are the steps you should be able to use to install. There’s a more detailed walkthrough with some of the error messages I saw underneath.

    brew install cabal-install
    cabal update
    cabal install cabal-install
    cabal install syb
    git clone https://github.com/koalaman/shellcheck.git
    cd shellcheck
    cabal install

Then stick `export PATH=$HOME/.cabal/bin:$PATH` in your .bash_profile (or similar) and you're done. Now you can run `shellcheck script/test/unit/TEST_compare-versions.sh` and get output like the below! I got many more problems reported, but I didn’t think you’d want to read them all…

```
…
In script/test/unit/TEST_compare-versions.sh line 60:
	successTestResult $TEST_NAME
                          ^-- SC2086: Double quote to prevent globbing and word splitting.
…
```

In fact that’s a great example of something that catches me out a lot. Also, the exit code will indicate an error, so you can even put this in you CI build to make sure you get fast feedback when you do something silly. The script can take a number of file arguments, and works with globbed paths. If any of the files specified have issues then the exit code will indicate this, so you just need to run something like `shellcheck *.sh` to see whether you have any problems.

It might even be a useful tool to make available to your continuous integration systems to provide fast feedback to developers working on shell scripts.

# Detailed Walkthrough

Install cabal

```
mark.crossfield@Galactica-Actual  ~ $ brew install cabal-install
==> Installing dependencies for cabal-install: apple-gcc42, ghc
==> Installing cabal-install dependency: apple-gcc42
==> Downloading https://downloads.sf.net/project/machomebrew/Bottles/apple-gcc42-4.2.1-5666.3.mavericks.bottle.2.tar.gz
######################################################################## 100.0%
==> Pouring apple-gcc42-4.2.1-5666.3.mavericks.bottle.2.tar.gz
==> Caveats
NOTE:
This formula provides components that were removed from XCode in the 4.2
release. There is no reason to install this formula if you are using a
version of XCode prior to 4.2.

This formula contains compilers built from Apple's GCC sources, build
5666.3, available from:

  http://opensource.apple.com/tarballs/gcc

All compilers have a `-4.2` suffix. A GFortran compiler is also included.
==> Summary
🍺  /usr/local/Cellar/apple-gcc42/4.2.1-5666.3: 104 files, 75M
==> Installing cabal-install dependency: ghc
==> Downloading https://downloads.sf.net/project/machomebrew/Bottles/ghc-7.6.3.mavericks.bottle.2.tar.gz
######################################################################## 100.0%
==> Pouring ghc-7.6.3.mavericks.bottle.2.tar.gz
==> Caveats
This brew is for GHC only; you might also be interested in haskell-platform.
==> Summary
🍺  /usr/local/Cellar/ghc/7.6.3: 5286 files, 776M
==> Installing cabal-install
==> Downloading https://downloads.sf.net/project/machomebrew/Bottles/cabal-install-1.18.0.2.mavericks.bottle.1.tar.gz
######################################################################## 100.0%
==> Pouring cabal-install-1.18.0.2.mavericks.bottle.1.tar.gz
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/cabal-install/1.18.0.2: 5 files, 18M
```

Next get the ShellCheck source

```
mark.crossfield@Galactica-Actual  ~/Documents/workspace $ git clone https://github.com/koalaman/shellcheck.git
Cloning into 'shellcheck'...
remote: Reusing existing pack: 1661, done.
remote: Counting objects: 8, done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 1669 (delta 1), reused 0 (delta 0)
Receiving objects: 100% (1669/1669), 628.89 KiB | 416.00 KiB/s, done.
Resolving deltas: 100% (877/877), done.
Checking connectivity... done.
```

Try installing ShellCheck

```
mark.crossfield@Galactica-Actual  ~/Documents/workspace $ cd shellcheck/
mark.crossfield@Galactica-Actual  ~/Documents/workspace/shellcheck $ cabal install
Config file path source is default config file.
Config file /Users/mark.crossfield/.cabal/config not found.
Writing default configuration to /Users/mark.crossfield/.cabal/config
Warning: The package list for 'hackage.haskell.org' does not exist. Run 'cabal
update' to download it.
Resolving dependencies...
cabal: Could not resolve dependencies:
trying: ShellCheck-0.3.2 (user goal)
next goal: regex-compat (dependency of ShellCheck-0.3.2)
Dependency tree exhaustively searched.
```

As instructed, update Cabal’s package list.

```
mark.crossfield@Galactica-Actual  ~/Documents/workspace/shellcheck $ cabal update
Downloading the latest package list from hackage.haskell.org
Note: there is a new version of cabal-install available.
To upgrade, run: cabal install cabal-install
```

Then update cabal-install itself (probably should have run a brew update before running `brew install cabal-install`?)

```
mark.crossfield@Galactica-Actual  ~/Documents/workspace/shellcheck $ cabal install cabal-install
Resolving dependencies...
Downloading Cabal-1.18.1.3...
Downloading random-1.0.1.1...
Downloading stm-2.4.3...
Configuring random-1.0.1.1...
Downloading transformers-0.3.0.0...
Configuring Cabal-1.18.1.3...
Configuring stm-2.4.3...
Downloading zlib-0.5.4.1...
Downloading text-1.1.0.1...
Configuring transformers-0.3.0.0...
Configuring zlib-0.5.4.1...
Configuring text-1.1.0.1...
Building zlib-0.5.4.1...
Building stm-2.4.3...
Building random-1.0.1.1...
Building text-1.1.0.1...
Building transformers-0.3.0.0...
Installed stm-2.4.3
Installed zlib-0.5.4.1
Installed random-1.0.1.1
Installed transformers-0.3.0.0
Downloading mtl-2.1.3.1...
Configuring mtl-2.1.3.1...
Building mtl-2.1.3.1...
Installed mtl-2.1.3.1
Building Cabal-1.18.1.3...
Installed text-1.1.0.1
Downloading parsec-3.1.5...
Configuring parsec-3.1.5...
Building parsec-3.1.5...
Installed parsec-3.1.5
Downloading network-2.4.2.2...
Configuring network-2.4.2.2...
Building network-2.4.2.2...
Installed network-2.4.2.2
Downloading HTTP-4000.2.12...
Configuring HTTP-4000.2.12...
Building HTTP-4000.2.12...
Installed HTTP-4000.2.12
Installed Cabal-1.18.1.3
Downloading cabal-install-1.18.0.3...
Configuring cabal-install-1.18.0.3...
Building cabal-install-1.18.0.3...
Installed cabal-install-1.18.0.3
```

Try installing ShellCheck again.

```
mark.crossfield@Galactica-Actual  ~/Documents/workspace/shellcheck $ cabal install
Resolving dependencies...
Downloading regex-base-0.93.2...
Downloading syb-0.4.1...
Configuring regex-base-0.93.2...
Configuring syb-0.4.1...
Failed to install syb-0.4.1
Last 10 lines of the build log ( /Users/mark.crossfield/.cabal/logs/syb-0.4.1.log ):
Configuring syb-0.4.1...
setup-Cabal-1.18.1.3-x86_64-osx-ghc-7.6.3:
/var/folders/mq/lsxl0jld03b8qmprt4jtfkcrkyg7pc/T/26151.o: does not exist
Building regex-base-0.93.2...
Installed regex-base-0.93.2
Downloading regex-posix-0.95.2...
Configuring regex-posix-0.95.2...
Building regex-posix-0.95.2...
Installed regex-posix-0.95.2
Downloading regex-compat-0.95.1...
Configuring regex-compat-0.95.1...
Building regex-compat-0.95.1...
Installed regex-compat-0.95.1
cabal: Error: some packages failed to install:
ShellCheck-0.3.2 depends on syb-0.4.1 which failed to install.
json-0.7 depends on syb-0.4.1 which failed to install.
syb-0.4.1 failed during the configure step. The exception was:
ExitFailure 1
```
<a name="syb"></a>
The syb dependency failed to install, but it worked when I installed it directly:

```
mark.crossfield@Galactica-Actual  ~/Documents/workspace/shellcheck $ cabal install syb
Resolving dependencies...
Configuring syb-0.4.1...
Building syb-0.4.1...
Installed syb-0.4.1
```

Now try the ShellCheck install again…

```
mark.crossfield@Galactica-Actual  ~/Documents/workspace/shellcheck $ cabal install
Resolving dependencies...
Downloading json-0.7...
Configuring json-0.7...
Building json-0.7...
Installed json-0.7
Configuring ShellCheck-0.3.2...
Building ShellCheck-0.3.2...
Installed ShellCheck-0.3.2
```

Success! \o/
