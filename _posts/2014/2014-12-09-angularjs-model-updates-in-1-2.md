---
id: 686
title: Angular Model Updates on blur in 1.2
date: 2014-12-09T13:54:51+00:00
author: Matt Erickson (ME)
layout: post
permalink: /angularjs-model-updates-in-1-2/
spacious_page_layout:
  - default_layout
categories:
  - Development
  - Javascript
  - Web
---
Why must we do this So, due to some business limitations, and much to my chagrin, I am supporting IE8 at work. I don&#8217;t even want to talk about it. BUT with that we also want to not be &#8220;bossy&#8221; in the way we show users errors in our angular code. Brings me to the point; custom angular directive to polyfill the 1.2 -> 1.3 gap in modelOptions! (also not happy to change the core of angular in this way). 

### Angular Code time! Get the angular module (or create) 

```javascript
var module = app.module('myNeatDirectives');
```
Create the angular directive. We use &#8216;input&#8217; because we don&#8217;t want opt in function here, we don&#8217;t even want opt out now (that can be added). We also restrict to &#8216;E&#8217; which is element (i.e. <input type=&#8221;text&#8221; />). We require ngModel (<input type=&#8221;text&#8221; />) but throw the &#8216;?&#8217; on there for optional inclusion. Finally setting the priority to 99 so it runs after the angular binding happens. 

```javascript
module.directive('input', ['$sniffer', function ($sniffer) {
    return {
        restrict: 'E',
        require: '?ngModel',
        priority: 99,
```
Next up, the bread and butter. We check if the input is of type radio or check box, no need to do special bindings there: return; Then we use angular&#8217; built in $sniffer to check for event bindings, in a similar fashion to how modernizr would work, unbind any bound events from the element. 

```javascript
link: function (scope, elm, attr, ngModelCtrl) {
            if (attr.type === 'radio' || attr.type === 'checkbox') return;
            if ($sniffer.hasEvent('input')) {
                elm.unbind('input');
            }
            if ($sniffer.hasEvent('change')) {
                elm.unbind('change');
            }
            if ($sniffer.hasEvent('keydown')) {
                elm.unbind('keydown');
            }
```
Now we bind up our blur events and update the model.$viewValue on the blur callback. 

```javascript
elm.bind('blur', function () {
                if (ngModelCtrl.$viewValue === elm.val()) {
                    return;
                }
                scope.$apply(function () {
                    ngModelCtrl.$setViewValue(elm.val());
                });
            });
```
There are some cases (search boxes) that you may want a specific keypress to trigger events. I wanted enter to also set the value, so boom. Made it happen. 

```javascript
elm.bind("keydown keypress", function (event) {
                var charCode = event.which || event.keyCode;
                if (charCode === 13) { //enter key is 13
                    scope.$apply(function () {
                        ngModelCtrl.$setViewValue(elm.val());
                    });
                }
             });
//and close the rest of the curlies and squares
        }
    };
}]);
```