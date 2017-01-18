---
title: A simple way to kill the annoying custom theming in angular material
date: 2017-01-17T23:56:00+00:00
author: Matt Erickson (ME)
layout: post
permalink: /angular-material-theming-(or_not)/
spacious_page_layout:
  - default_layout
categories:
  - Development
  - HTML
  - JavaScript
  - Angular
---
Welcome back!
=====
Ok, maybe I'm saying that to myself.  In either case, long time no talk, internet!  Today we have a quick trick to kill styling in angular-material, which is a framework for angular 1 or 2 that I have enjoyed [link to angular-material](https://material.angularjs.org). So, here's the thing, we (at my work) have a large code base that already has a multi tenent implementation of different themes set and we didn't implement that using material (wasn't available 4 years ago).  So when we started pulling in pieces and including javascript we started noticing things like `a:not(.md-button)` and `.md-default-theme` popping up around, to our surprise. Up until recently it hadn't been a problem... well, you guessed it, it became a problem.  We had a few buttons from our old bootstrap days with `btn btn-link` that should have been a specific color for a theme and they were being overridden.  Took some digging but there was some dynamically generated CSS that was being shimmed into the `<head>` of the HTML.  We found a way around this though, straight from the docs, check it out: [Disable Theming](https://material.angularjs.org/1.1.1/Theming/03_configuring_a_theme#disable-theming).  **Note: this __JUST__ became a thing in version 1.1.1!!!**  Upgrade, for God's sake!

This change is relatively minimal to stop the theming from getting injected.  You inject `$mdThemingProvider` into your app config and then call the function `disableTheming();` Now i will mention that we are passing a true as the code itself looks to pass that so we followed suit, worst case it gets ignored.

```javascript
angular.module('myApp', ['ngMaterial'])  
  .config(function($mdThemingProvider) {  
    $mdThemingProvider.disableTheming();  
  });  
```

Well, that is all I have for today.  God's speed.