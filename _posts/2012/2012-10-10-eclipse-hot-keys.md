---
id: 38
title: Eclipse Hot-Keys
date: 2012-10-10T21:06:13+00:00
layout: post
permalink: /eclipse-hot-keys/
categories:
  - Development
tags:
  - eclipse
  - hacking
  - hot-key
  - quick
  - typing
---
Note: _This information is meant to be generic to Eclipse as a whole but for reference I run ubuntu 10 and eclipse Helios Service Release 2_ 

# Eclipse In the company I work for we use 

<a href="http://www.eclipse.org/" rel="external">Eclipse</a> as our primary IDE for development. Eclipse is a project by &#8220;The Eclipse Foundation&#8221;. It is an IDE that has MANY, many plug-ins that range from official ones such as the <a href="http://www.jboss.org/tools/download" rel="external">JBoss plugin</a> to make using jboss technologies like drools rules easier to work with to from within eclipse to <a href="http://andrei.gmxhome.de/anyedit/" rel="external">AnyEdit</a> which is something I use to remove trailing spaces and tabs from my code (for checkstyle purposes) 

### Hot-Keys By using Eclipse efficiently you can decrease the amount of time you spend on tedious things and increase your productivity significantly Firstly, moving quickly without letting your hands leave the keyboard can speed you up more than you would expect. So lets look at some of those hot-keys, most of which are built into OS&#8217;. 

<div class="smallMargin">
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+c :copy
Ctrl+v :paste
Ctrl+x :cut
Ctrl+z :undo
Ctrl+y :redo</pre>
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+(arrow key [left or right]) </pre> will move the corresponding direction one word, if you are using programming standard camel-case variables this will move you one word and stop at the beginning or end of the word you are moving over.
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Shift+(arrow key [left or right]) </pre> will move the corresponding direction one space and highlight the space you moved over.
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+Shift+(arrow key [left or right]) </pre> will work as you might expect, moving one word the corresponding direction AND highlight the word.
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+Shift+r </pre> will open an &#8216;Open Resource&#8217; window that allows you to quickly search your workspace. Inside of this search you can use &#8216;*&#8217; to get a wildcard for any string forward or backward or &#8216;?&#8217; for any char. Example: applicationContext-ws-stuff.xml could be found by searching app*con*ws-stuff* or even shorter as app*con*stuff* may give you a short list. Again if you are using camel-case you can use just the FIRST-LETTER of the word. Example: java file: TeacherToStudent.java could be found by typing TTS.
  
  <br /><br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+Shift+t</pre> will open an &#8216;Open by Type&#8217; window that works essentially the same as the Open Resource window
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+Shift+m and Ctrl+Shift+o </pre> these two hot-keys are nearly the same, +m will add any existing imports that are missing and +o will add any missing ones and then organize them based on how you have your code-style defined
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Alt+Shift+r </pre> a powerful key combo. This is the variable or method refactor tool in hot-key form!
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+o </pre> another very useful hot-key this will open a small search window for the class you are currently in, you can search for variables or methods quickly and reach them even faster!
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Shift+(home or end) </pre> this will highlight the space from your cursor (where ever it may be) to the end or beginning of the LINE you are on.
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+i </pre> will correct the indentation of the file, if you have a line or section of code highlighted it will respect this highlighting and only correct indentation of THAT section or line of code!
  
  <br /> 
  
  <pre class="brush: plain; title: ; notranslate" title="">Ctrl+d </pre> will delete the line you are on, again if you have a section of code or space highlighted ALL of it will be deleted
  
  <br /> An honorable mention, although not a hot-key, is the 
  
  <pre class="brush: plain; title: ; notranslate" title="">'Replace with Local History' and 'Compare with Local History'</pre> menu items. There have been many times when I changed a significant amount of code only to come back the next day to realize that everything is broken and I have no idea what the method/class I changed was supposed to do. Well this is where your butt will be saved. Right Click the class you changed->Compare/Replace With->Local History will bring up a new menu that will show you past changes (saying it has the history still stored). This has saved my butt in the past and I&#8217;m sure it will again in the future. I know a lot of these seem like they may be useless and trivial clicks but once you get used to using them you will be able to move so quickly through your files and eclipse that you will never fall out of &#8216;programming mode&#8217; having to copy, paste things around a file.
</div>