---
id: 570
title: window.Browser?
date: 2014-06-06T13:02:18+00:00
author: Matt Erickson (ME)
layout: post
permalink: /window-browser/
categories:
  - HTML5/CSS3
  - Javascript
  - Web
tags:
  - Hack
  - IE
  - IIFE
  - javascript
  - jquery
---
We all love IE, right?!? WRONG! Well now with jquery bumping out the browser detection we have to have some way to deal with IE and gracefully degradating our features. I found a pretty neat way of dealing with browser detection that I have integrated at a very root layer for my javascript. 

<pre class="brush: jscript; title: ; notranslate" title="">(function (window, navigator) {
    window.Browser = {
        IsIe: function () {
            return navigator.appVersion.indexOf("MSIE") !== -1;
        },
        IsIeMobile10: function () {
            return navigator.userAgent.match(/IEMobile\/10\.0/);
        },
        Navigator: navigator.appVersion,
        Version: function () {
            var version = 999; // we assume a sane browser
            if (navigator.appVersion.indexOf("MSIE") !== -1) {
                // bah, IE again, lets downgrade version number
                version = parseFloat(navigator.appVersion.split("MSIE")[1]);
                return version;
            }
        }
    };
}(window, navigator));
</pre> Let&#8217;s pick this guy apart, shall we? First off, we wrap the whole thing an Immediately-Invoked Function Expression, or IIFE (if-ee). This lets us get some immediate functionality as soon as the JS is hit, it also, based on the params passed into the function, have local references to object that live on the js page scope so there is much faster retrieval time. 


  
E.G.
  


<pre class="brush: jscript; title: ; notranslate" title="">(function (yellowSubmarine) {
    yellowSubmarine.on('click', function(event) {
        console.log("do click things");
    });
}(jQuery));
</pre> This will set the var \`yellowSubmarine\` to the jQuery function. Pretty normal javascript pattern. Moving on.


  

  
We grab \`window\` and set a new variable on it named \`Browser\`. This is where we will store our helper methods to figure out if we are dealing with IE or not. \`IsIe\`, \`IsIeMobile10\`, \`Navigator\`, and \`Version\` are all helper functions that can now be called off of \`window.Browser\` or just \`Browser\` from JS. If we have a piece of functionality that we want removed that isn&#8217;t capable of being detected by any other technology that has been implemented we now have a simple and concise way to detect and turn it off!
  

  
For example; in the previous post I wrote about the custom select box and mentioned that it will not work in IE8-10. Here is how i chose to disable it using the example code above: 

<pre class="brush: jscript; title: ; notranslate" title="">$(function() {
    if (window.Browser.IsIe() && window.Browser.Version() &lt;= 10) {
        var selectBoxes = $(".custom-select-box");
        for (var i = 0; i &lt; selectBoxes.length; i++) {
            $(selectBoxes[i]).removeClass("custom-select-box full-width").attr("style", "width:100%").find("select").removeClass("form-control").attr("style", "width:100%");
        }
    }
};
</pre> No regex, easily readable. One line, two condition if statement. Doesn&#8217;t get much better than that in terms of detecting and fixing IE. This fix was to &#8216;gracefully degradate&#8217; IE10-IE8 (our supported browsers) by just disabling the custom styling. DONE!