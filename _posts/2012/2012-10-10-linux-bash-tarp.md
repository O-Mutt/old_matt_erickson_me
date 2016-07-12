---
id: 50
title: Linux Bash TARP!
date: 2012-10-10T21:20:51+00:00
layout: post
permalink: /linux-bash-tarp/
categories:
  - Linux
  - OS
tags:
  - bash
  - linux
  - terminal
  - terminal title
---
So I was trying to pull a log file from a sys admin at my work&#8217;s computer the other day with scp. 

### Fail. Fail. Fail. Fail.  Have a linux admin try from my computer under his account worked fine. Turns out that something in my .bashrc was causing output when logged into another computer and breaking scp but doesn&#8217;t break ssh&#8230; Go figure?!? Anyway, passed that I found a fairly sweet command that I now have living in my .bashrc file: 

<pre class="brush: bash; title: ; notranslate" title="">trap 'echo -e "\e]0;$BASH_COMMAND&#92;&#48;07"' DEBUG</pre> Still working out exactly how it is doing what it is doing but I know the outcome: When I run a command in my terminal, the title of that terminal/tab changes to the command I just ran! Very useful when you are tailing 5 different log files and just want to find that dang web-services log without having to actually read what the log is telling you!