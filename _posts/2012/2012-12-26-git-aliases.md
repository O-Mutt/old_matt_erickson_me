---
id: 283
title: Git Aliases
date: 2012-12-26T11:37:40+00:00
author: Matt Erickson (ME)
layout: post
guid: http://matterickson.me/?p=283
permalink: /git-aliases/
categories:
  - Development
  - Git
  - Linux
tags:
  - aliases
  - Git
---
So, it has been a while but I have been working hard so we all know that you can&#8217;t really blame me for that!  


  
So today I want to run down my git configuration and how i make my life easier by using aliases&#8230; which if you haven&#8217;t guessed yet, I LOVE!  


  
So here we go:  


  
This is all in my ~/.gitconfig file
  
(Notes will be denoted by &#8216;##&#8217; and are meant to explain the NEXT line)  


  


<pre class="brush: bash; title: ; notranslate" title="">[user]
  name = Matthew Erickson
  email = matt@matterickson.me
[color]
  branch = auto
  diff = auto
  interactive = auto
  status = auto
[alias]
  ##Shows all aliases
  aliases = !git config --get-regexp 'alias.*' | colrm 1 6 | sed 's/[ ]/ = /'
  ## Pretty log (don't forget a -n XX to only show XX amount of commits)
  lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset 
%s %Cgreen(%cr) %C(bold blue)&lt;%an&gt;%Creset' --abbrev-commit --date=relative
  ## Formats a patch without using whitespace
  format-patch = format-patch -w
  ## Same as above but for term diffs
  diff = diff -w
  ## Quick status
  st = status
  ## Quick rebase
  rb = rebase
  ## Creates a new branch tracking the current one
  bk = checkout --track -b
  ## Quick branch
  br = branch
  ## Quick Checkout
  ck = checkout
  ## Quick pull w/rebase
  puller = pull --rebase
  ##is supposed to push for the branch refs
  pushup = "!f() { git push -u ${1:-origin} HEAD:`git config branch.
$(git name-rev --name-only HEAD).merge | sed -e 's@refs/heads/@refs/for/@'`; }; f"
  ##fetch and rebase on master
  up = !git fetch origin && git rebase origin/master
  ## Shows the top contributers and how many commits they have w/o merges
  who = shortlog -n -s --no-merges
  ## Cleans up git configs (should not be done while in a working state)
  cleanup = !git remote prune origin && git gc && git clean -dfx && git stash clear
  ## Shows new info from last command (usually after a git pull or git puller)
  new = !sh -c 'git log $1@{1}..$1@{0} "$@"'
  ## Shows branch tracking information
  track = "!f() { ([ $# -eq 2 ] && ( echo \"Setting tracking for branch \" $1 \" -&gt; \" $2;
git branch --set-upstream $1 $2; ) || ( git for-each-ref --format=\"local: %(refname:short) 
&lt;--sync--&gt; 
remote: %(upstream:short)\" refs/heads && echo --Remotes && git remote -v)); }; f"
</pre>