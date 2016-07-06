---
id: 553
title: Custom Styled HTML dropdown/select boxes
date: 2014-06-05T10:32:38+00:00
author: Matt Erickson (ME)
layout: post
guid: http://matterickson.me/?p=553
permalink: /dropdowns_selectboxes/
spacious_page_layout:
  - default_layout
categories:
  - Featured
  - HTML5/CSS3
  - Web
tags:
  - CSS
  - Dropdown
  - HTML
  - Select
  - SelectBox
---

    <label class="custom-select-box full-width"> <select class="form-control"> <option value="1">Wow</option> <option value="2">this is</option> <option value="3">exactly what UX/UI</option> <option value="4">wanted this to look like!!!</option> </select> </label> UI/UX and dev is always a delicate balance. We had a recent request come in to style our dropdowns as the rest of our form fields. We are using bootstrap so our inputs are fairly customized. Here is how I did it, I will discuss the issues and caveats after the basic code for &#8220;modern&#8221; browsers.  


  
HTML structure
  


```html
    <select>
        <option value="1">Value 1</option>
        <option value="2">Value 2</option>
        <option value="3">Value 3</option>
        <option value="4">Value 4</option>
    </select>
</label>
```


  
This is all in less.
  

  
Style the containing label:
  


```css
.custom-select {
    position: relative;

    &:after {
        .fa; //Font awesome icon
        .input-group-addon; //bootstrap mixin
        border-bottom-left-radius: 0;
        border-top-left-radius: 0;
        padding: 10px 13px;
        width: auto;
        height: 100%;
        content: "\f107"; //down arrow
        font-family: FontAwesome;
        position: absolute;
        right: 15px;
        top: 0px;
        pointer-events: none; //Do not block the propagation of the pointer event
    }
```

Now to style the select box itself which is really just hiding the arrows and coloring it.

```css
select {
        outline: none; //hide the outline
        -webkit-appearance: none; //hide the arrows
        -moz-appearance: none; //hide the arrows
        appearance: none; //hide the arrows
        cursor: pointer; //change the cursor
        .placeholder(); //mixin for placeholder values
        color: @input-color; //theme var
        font-weight: normal;

        option {
            color: @input-color; //background for the options
        }
    }
    /* Targetting Webkit browsers only. FF will show the dropdown arrow with so much padding. */
    @media screen and (-webkit-min-device-pixel-ratio:0) {
        select {
            padding-right: 18px;
        }
    }
}
```


Relatively simple, but there are some key pieces that need to be in place for this to work.

  * `pointer-event: none;` This is very important or the overlaid addon would catch the pointer even and we wouldn't "click through" to the underlying select box. This is **NOT SUPPORTED** by anything less than IE11. (IE10 is still going to cause you fits here).
  * `outline: none; //hide the outline
  * -webkit-appearance: none; //hide the arrows 
  * -moz-appearance: none; //hide the arrows
  * appearance: none; //hide the arrows
  * cursor: pointer; //change the cursor
  Also very important so we don't see the stupid OS generated select boxes that change from one to the next.


  
You will probably also notice that I don&#8217;t touch any of the nasty hacks that could happen for IE8-10. This is because I used a bit of javascript to grab these boxes and just remove all custom styling. It is much easier than hacking it and we have decided it to be graceful degradation. I will discuss this in a different post. 
  
Your output should look something like this:
  

<img src="https://raw.githubusercontent.com/Mutmatt/mutmatt.github.io/master/images/custom_select-300x28.png?fit=300%2C28" alt="Custom_Select" class="alignnone size-medium wp-image-554" srcset="https://raw.githubusercontent.com/Mutmatt/mutmatt.github.io/master/images/custom_select.png?zoom=2&resize=600%2C60 1200w, https://raw.githubusercontent.com/Mutmatt/mutmatt.github.io/master/images/custom_select.png?zoom=3&resize=600%2C60 1800w" sizes="(max-width: 600px) 100vw, 600px" data-recalc-dims="1" /> 
  
Unlike some examples i&#8217;ve seen out on the internet here is an actual WORKING example of how this is supposed to look and behave in modern browsers. 

<label class="custom-select-box full-width"> <select class="form-control"> 
  <option value="1">Value 1</option> <option value="2">Value 2</option> 
  <option value="3">Value 3</option> <option value="4">Value 4</option>
  </select>
</label> 

<link href="//netdna.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css" rel="stylesheet" />