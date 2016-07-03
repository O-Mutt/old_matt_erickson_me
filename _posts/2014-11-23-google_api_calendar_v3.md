---
id: 666
title: Google Api v3 Migration
date: 2014-11-23T21:00:58+00:00
author: Matt Erickson (ME)
layout: post
guid: http://matterickson.me/?p=666
permalink: /google_api_calendar_v3/
spacious_page_layout:
  - default_layout
categories:
  - Development
  - Featured
  - PHP
  - Web
tags:
  - google api
  - google calendar
  - google calendar api
  - google php api
  - PHP
---
## Google Api v1/v2 is dead, move on

**Please note the Google PHP Api changes regularly and none of this code is future proof as the google api client is still in beta**  

  
Recently I undertook a php application that was using a &#8216;zend&#8217; google calendar api. Well as of the 17th of November 2014 the google api v1/2 (used internally by zend) shut down. I used this as a learning opportunity to impl google api v3.   

  
So here is the code that I have come up with that has worked pretty well for me. It is very similar to zend.   

  
First we setup our google client from the client implementation on <a href="https://github.com/google/google-api-php-client" title="Google-Api-Php-Client" target="_blank">Google Api Php Client</a>, you will need the client in your application somewhere and will need to require the AutoLoad.php in order to use it. (Not shown below) 

## Code it out

<pre class="brush: php; title: ; notranslate" title="">$user = 'useremail@gmail.com';
   
$gclient = new Google_Client();
$gclient-&gt;setApplicationName("My Apps Name");
$gclient-&gt;setClientId("**crazy_string_here**apps.googleusercontent.com");

if (isset($_SESSION[$user.'_service_token'])) {
	$gclient-&gt;setAccessToken($_SESSION[$user.'_service_token']);
}
$key = file_get_contents($privateKeyLocation);
$auth = new Google_Auth_AssertionCredentials(
	$config-&gt;google_email_address, //this is my service account email **crazy_string_here**@developer.gserviceaccount.com
	array('https://www.googleapis.com/auth/calendar'),//Google calendar permissions
	$key //contents of my .p12 file i downloaded from console.developers.google.com
);
$auth-&gt;sub = $user;//This is saying our service account will be acting as the sub user
$gclient-&gt;setAssertionCredentials($auth);
if ($gclient-&gt;getAuth()-&gt;isAccessTokenExpired()) {
	$gclient-&gt;getAuth()-&gt;refreshTokenWithAssertion($auth);
}
$_SESSION[$user.'_service_token'] = $gclient-&gt;getAccessToken();
</pre> At this point we have setup all of our google_client code so we can add our implemented &#8220;add calendar event&#8221;. First Instantiate the calendar service. 

<pre class="brush: php; title: ; notranslate" title="">$cal_service = new Google_Service_Calendar($gclient);
</pre> Now we need to set up an event, give it a &#8220;summary&#8221;, location, and a start and end datetime in format 

<pre class="brush: php; title: ; notranslate" title="">"YYY-MM-DDTHH:MM:SS.MMM+0001"
</pre> or 

<pre class="brush: php; title: ; notranslate" title="">datetime-&gt;format('Y-m-d\TH:i:s.000P')
</pre>

<pre class="brush: php; title: ; notranslate" title="">$event = new Google_Service_Calendar_Event();
	$event-&gt;setSummary("Event Title");
	$event-&gt;setLocation("123 Fake St. Dover, ME 41426");//Address City, State Zip
	$event-&gt;setDescription("You have a new event on your calendar!");
	$endTime = clone $aDateTimeObject;
	$endTime-&gt;add(new DateInterval('PT1H'));//1 hour calendar event
	
	$start = new Google_Service_Calendar_EventDateTime();
	$start-&gt;setDateTime($aDateTimeObject-&gt;format('Y-m-d\TH:i:s.000P'));
	$event-&gt;setStart($start);
					
	$end = new Google_Service_Calendar_EventDateTime();
	$end-&gt;setDateTime($endTime-&gt;format('Y-m-d\TH:i:s.000P'));
	$event-&gt;setEnd($end);
					
	$createdEvent = $cal_service-&gt;events-&gt;insert($user, $event);
</pre> At this point we have a calendar event returned to us and can use 

<pre class="brush: php; title: ; notranslate" title="">$createdEvent-&gt;id
</pre> to get the event ID if we want to store it so it can be updated/deleted later in similar fashion like so: 

<pre class="brush: php; title: ; notranslate" title="">$cal_service-&gt;events-&gt;delete($user, $createdEvent-&gt;id);
</pre> Hopefully this was enlightening for you and with all the recent changes (and shutdowns) of the google api this can help you transition your application more quickly to the new version.