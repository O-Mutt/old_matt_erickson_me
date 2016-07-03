---
id: 52
title: Another Lesson Learned in Drools
date: 2012-10-10T21:29:28+00:00
layout: post
guid: http://matterickson.me/?p=52
permalink: /another-lesson-learned-in-drools/
categories:
  - Development
  - Java
tags:
  - business rules
  - drools
  - java
  - jboss
---
<div class="separator" style="clear: both; text-align: center;">
  <a href="http://i0.wp.com/lh6.googleusercontent.com/-yI_NwSc7pc8/UCFRLmax5KI/AAAAAAAAB1w/jBTweZhnNlo/s371/2012-08-07_13-30-38_996.jpg?ssl=1" imageanchor="1" style="clear:right; float:right; margin-left:1em; margin-bottom:1em" rel="external"><img border="0" src="http://i0.wp.com/lh6.googleusercontent.com/-yI_NwSc7pc8/UCFRLmax5KI/AAAAAAAAB1w/jBTweZhnNlo/s371/2012-08-07_13-30-38_996.jpg?resize=209%2C371&#038;ssl=1" data-recalc-dims="1" /></a>
</div> So, today, again, I was working with jboss&#8217; drools engine writing some more rules. My rule went something like this: 

<div class="thin">
  <pre class="brush: java; title: ; notranslate" title="">
rule "Do stuff"
  when
    $obj : Class(name == "")
  then
    $obj.somethingElse.setValue("More Stuff")//I did more stuff
end
</pre>
</div> So according to the docs this should work fine&#8230;.. well mine is broken. And non the less the //I did more stuff is what broke it. For reference, I am using Drools 5.1.0.M1, which, I know, is NOT the docs that I am pointing you to but I would assume that commenting should be the same! 

<a href="http://docs.jboss.org/drools/release/5.2.0.Final/drools-expert-docs/html_single/" rel="external">DroolsDocs#Single_Line_Comment</a>