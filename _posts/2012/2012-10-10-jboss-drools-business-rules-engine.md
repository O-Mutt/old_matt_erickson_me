---
id: 32
title: Jboss Drools Business Rules Engine
date: 2012-10-10T21:01:31+00:00
layout: post
guid: http://matterickson.me/?p=32
permalink: /jboss-drools-business-rules-engine/
categories:
  - Java
tags:
  - business rules
  - drools
  - java
  - tutorial
---
So, I have had the luxury of working with just under a butt load of technologies at in my young software engineering career. One that I have enjoyed more than others has been <a href="http://www.jboss.org/drools/" rel="external">Jboss&#8217; own Drools Rules Engine</a>. This engine allows you to quickly and &#8220;easily&#8221; integrate complex business rules into your application without muddling them into your actual application layer. 

<div class="smallMargin">
  So the drools syntax can be a bit confusing at first glance but after you write a few simple rules and see how they work it is cake! 
  
  <div>
    Ex:
  </div>
  
  <pre class="brush: java; title: ; notranslate" title="">
rule "This is a short description of the rule"
when
$derp : MyObject(name == "Matt")
then
$derp.lastName.setValue("Erickson")
end
</pre>
  
  <div>
    Lets break that down line by line:
  </div>
  
  <div>
    <strong><span style="text-decoration: underline;">Line 1:</span></strong> rule &#8220;blah blah blah&#8230;&#8221; &#8211; This explains what the rule does, it doesn&#8217;t actually have to explain anything but must be unique to this rules engine or it will bomb out.
  </div>
  
  <div>
    <span style="font-weight: bold; text-decoration: underline;">Line 2:</span>when &#8211; indicates this is the left hand side of the rule (until we reach a then statement).
  </div>
  
  <div>
    <span style="font-weight: bold; text-decoration: underline;">Line 3:</span>$derp : MyObject(name == &#8220;Matt&#8221;) &#8211; This is actually where the rule&#8217;s business logic lives for determining if we should run the right hand side logic on this object. This line is <strong>VERY </strong>important. The &#8216;$variableName&#8217; notation is common in drools but is notnecessarily, we can just use &#8216;derp&#8217; as a variable but you can see why we don&#8217;t, forreadabilitysake. The &#8216;:&#8217; item is a MUST, this is actually what assigns the object to the variable when the rules match. This is the part of drools that is kinda Quirky, if a new line is added. Say we insert a line AFTER line 3, we&#8217;ll call it 4a (for line 4 alternative):
  </div>
  
  <pre class="brush: java; title: ; notranslate" title="">MyObject(age &gt; 23)</pre>
  
  <div>
    This line will ask the very same &#8216;MyObject&#8217; if it <em style="font-weight: bold;">ALSO</em> has an age attribute that is greater than 23.
  </div>
  
  <div>
    Before we move on I would like to look at a few ways this line can be modified to have the same behavior. Lets remove line 4a and append that logic to line 3:
  </div>
  
  <pre class="brush: java; title: ; notranslate" title="">$derp : MyObject(name == "Matt" &amp;&amp; age &gt; 23)</pre>
  
  <div>
    Simple enough. Here is another:
  </div>
  
  <pre class="brush: java; title: ; notranslate" title="">$derp : MyObject(name == "Matt")
and MyObject(age &gt; 23)</pre>
  
  <div>
    This is nearly identical to 4a but with more explicit definition of what we want out of this rule. Drools, by default, treats new lines in the left hand side of a rule as &#8216;AND&#8217; statements. So this can be left out or added as you see fit, I would pick one and stick with it though. Similarly we can change the behavior with an &#8216;||&#8217; and an &#8216;or&#8217;. Ex.
  </div>
  
  <pre class="brush: java; title: ; notranslate" title="">$derp : MyObject(name == "Matt" ||age &gt; 23)
$derp : MyObject(name == "Matt")
or MyObject(age &gt; 23)</pre>
  
  <div>
    These are fairly self explanatory after learning how the and works.
  </div>
  
  <div>
    <span style="font-weight: bold; text-decoration: underline;">Line 4:</span>then &#8211; I&#8217;m sure by now you can guess what this does, indicates that if all left hand side arguments match: do this stuff.
  </div>
  
  <div>
    <span style="font-weight: bold; text-decoration: underline;">Line 5:</span>$derp.lastName.setValue(&#8220;Erickson&#8221;) &#8211; This is where the right hand side runs if all the left hand side arguments match. The &#8216;$derp&#8217;, here, is the same as the object that we set in the left hand side of the rule, this means we already have values in some of the object and don&#8217;t need to reset them&#8230; unless that is what the rules should do, of course. &#8216;.lastName&#8217; is anattributefrom the MyObject type with a &#8216;setValue&#8217; method that takes in a String.
  </div>
  
  <div>
    <span style="font-weight: bold; text-decoration: underline;">Line 6:</span> end &#8211; Fine!
  </div>
  
  <div>
    Now that you have &#8216;read&#8217; this you can probably go hack away at a keyboard and write something that may resemble a drools rule. But keep in mind; drools does not care the order in which you write your rules. It runs them much like a shotgun, all at once. So make sure you do not have any conflicting business rules!
  </div>
  
  <div>
    Things I didn&#8217;t cover that you should probably read further into: integration, knowledgeBase class, and most likely much much more but this was mostly from memory.
  </div>
</div>