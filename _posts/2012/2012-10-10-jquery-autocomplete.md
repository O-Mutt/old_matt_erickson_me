---
id: 48
title: 'jQuery UI Autocomplete with ajax&#8217;d custom JSONs'
date: 2012-10-10T21:17:04+00:00
layout: post
permalink: /jquery-autocomplete/
categories:
  - Web
tags:
  - ajax
  - autocomplete
  - custom object
  - javascript
  - jquery
  - jquery-ui
  - json
---
### Back story

So as of now you should probably already know what jquery is (javascript wrapper library to make it significantly easier to deal with and read) also JSON objects (much like maps [key: value]) and ajax (<a href="http://en.wikipedia.org/wiki/Ajax_(programming)" rel="external">ajax wiki -_-</a>). Well in this tutorial we are going to slam these all together.

### Technicals and Code

The code below will give you a straight forward look at a jQuery autocomplete text box. It is an input box and some jquery code to setup the box. Super simple&#8230; moving on.

<pre class="brush: jscript; title: ; notranslate" title="">&lt;head&gt;
  jQuery("#name").autocomplete({
    source: {'abc','def','ghi'....}
  });
&lt;/head&gt;
&lt;body&gt;
  &lt;input id="name"&gt;
&lt;/body&gt;
</pre>

Next we will only focus on the jquery aspect and add the ajax calls to our php/struts/asp whatever method

<pre class="brush: jscript; title: ; notranslate" title="">jQuery("#name").autocomplete( {
 source: function (request, response) {
   $.ajax({
     url: 'ENTER YOUR URL HERE',
     data: {
       searchTerm: request.term
       //'searchTerm' is what you are going to pull from the request
     },
     type: "POST",
     success: function(data) {
       //GREAT SUCCESS
     }
   });//end ajax
 }//end source of autocomplete
});
</pre>

This is still fairly straight forward. Once the custom JSON gets thrown into this mix is when we really start to feel like we are doing something. Lets start by looking at the JSON we build to send BACK to the page so we know what kind of data we are dealing with, then we can get rid of the &#8216;GREAT SUCCESS&#8217; comment

<pre class="brush: java; title: ; notranslate" title="">//Java
JSONArray array = new JSONArray();
JSONObject object = null;
for (CustomObj obj : m_objects) {
  object = new JSONObject();
  object.put("name", obj.getName());
  object.put("value", obj.getValue());
  object.put("year", obj.getYear());
  array.put(object);
}
//end Java
</pre>

<pre class="brush: jscript; title: ; notranslate" title="">//jQuery
//skipping autocomplete start and moving straight to success callback
success: function(data) {//data is the object that is returned
  response($.map(data, function(el) {
  //el is an element within the data object also known as our custom json object
    return {
      name: el.name,//corresponds with json object built above
      value: el.value,
      year: el.year
    }
  }));
}
//end jQuery
</pre>

The $.map is the function that really does the magic hear. It treats the response as a map and makes the new objects to return. In the return we build the object from the corresponding java JSON we built. We are mostly there now. All we have to do is tell jQuery what it should do with the values, since, by default it expects a label and a value.

<pre class="brush: jscript; title: ; notranslate" title="">jQuery("#name").autocomplete( {
.....
}).data("autocomplete")._renderItem = function(ul, item) {
  return $("&lt;li&gt;")
    .data("item.autocomplete", item)
    .append("&lt;a&gt;" + item.name + "&lt;/a&gt;")
    .appendTo(ul);
};
</pre>

This is a fairly straightforward function. It takes the data from the autocomplete._rederItem function and replaces it with our own function. The item in this case, referred to in the <a> with item.name, the .name refers to the object we created in the success callback. You could use anything you desired there (in our example here we can use .name, .value, or .year).

Hopefully this can help someone some time, thanks for reading