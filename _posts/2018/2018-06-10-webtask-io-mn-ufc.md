---
title: HTML scraping MN UFC's highlights page w/Webtask.io
date: 2018-06-10T12:00:00+00:00
author: Matt Erickson (ME)
layout: post
permalink: /webtask-io-mnufc/
spacious_page_layout:
  - default_layout
categories:
  - development
  - node
  - nodejs
tags:
  - webtask
  - webtask.io
  - node
  - development
---
WebTask.io, MN UFC, nodejs
=====
I have noticed something that you probably have as well. I have zero content for 2018... well save the one post about standups.
I want to and have done something about that. I recently learned about webtask.io, an [Auth0](auth0.com) product. It is a FaaS (function as a service) or serverless.
FaaS is a relatively new idea in the cloud computing space. It allows for development, running, managing and maintatining applications from a server-side perspective without the need to build out costly, (and from some perspectives) less interesting infrastructure.
The real use case for FaaS is when you have a known "on-demand" type request that you would like to run without the build out.
    - Streaming content
    - batch processing
    - IoT
Now to the nitty gritty.

MN UFC Html Scraping
====
I was looking for content to add to my site and, as some may know, I am a supporter of the Minnesota United Football Club (MNUFC).
So I thought to myself, why not show the highlights on my site? Enter [MN UFC Highlights Page](https://mnufc.com/video-channels/match-highlights). 
I decided this would be the perfect content to show. Simple, easy, eye catching, fun.

**TL;DR**: I use webtask.io to scrape the highlights for mnufc.com and commit each highlight as a new file to my jekyll site as a new posting. [MattErickson.me Repo](https://github.com/mutmatt/mutmatt.github.io), [MN UFC scraping webtask repo](https://github.com/Mutmatt/auto-pull-req-new-mnufc)

So I started with scraping the content, I knew I'd need `jquery` (or `cheerio` if you are in a `node` setting). I'd be making requests out so that was an easy 'grab'. Also `lodash` is usually an easy helper, `cheerio` as I mentioned, and `bluebird` to for help with the `request.all()`.

``` javascript
'use latest';//use es6

const request = require('request');
const rp = require('request-promise-native');
const _ = require('lodash');
const cheerio = require('cheerio');
const Promises = require('bluebird');
```

I'd need the non dynamic portion of the jekyll post header (see github pages) so:

``` javascript
let postHeader = `author: Matt Erickson (ME)
layout: post
categories:
  - MNUFC
  - Auto-post
tags:
  - MNUFC
  - Soccer
---`
```

and then on each highlight video page there is an embed link that looked the exact same, save a video ID:

``` javascript
let iframeUrlTemplate = `<div class='soccer-video-wrapper'>\r\n<iframe class='soccer-video' width='100%' height='auto' frameborder='0' allowfullscreen src="https://www.mnufc.com/iframe-video?brightcove_id={replaceMe}&brightcove_player_id=default&brightcove_account_id=5534894110001"></iframe>\r\n</div>`;
```

I added a keyword with some curries `{replaceMe}` to be replaced lated in the code.

Now the real code. I asked for the page's HMTL and did a transform on the response to load it into cheerio ($)

``` javascript
rp({
  uri: hostname + '/video-channels/match-highlights',
  transform: function(body) {
      return cheerio.load(body);
  }
})
```

Then I crawled the pages html for pieces that I was looking for. The title of the highlight, stripping out the word `HIGHLIGHT:` and any `apostrophes`. Stripping off the `pipe` and the date of the post and `any periods`. The title without spaces (mostly for the filename). The url of the highlight video page, this will be used to pull the ID I referenced earlier to get the video in an iframe on my site. And the date in javascript. I push all this info into a 'highlightArray' so we can use it again later. 

``` javascript
_.map($(".views-row .node"), 
  function(node) {
    let highlight = $(node).find('.node-title a');
    
    //Remove unneeded parts of the title that make things look weird
    let title = highlight.text().replace('HIGHLIGHTS: ', '').replace(/\'/gi, '');
    let titleWithoutEndDate = title.replace(/\|.*/gi, '').replace('\.', '');
    let titleWOEDAndSpaces = titleWithoutEndDate.replace(/\s/gi, '-').replace(/\-$/, '');
    let postUrl = highlight.attr('href');
    var date =  new Date($(node).find('.timestamp').text().replace(/\s\(.*\)/gi, ''));
    let filename = date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + '-' + titleWOEDAndSpaces + '.md';
    let permalink = _.snakeCase(filename);
    
    highlightArray.push({ 
        filename: filename,
        title: title, 
        postUrl: postUrl, 
        date: date,
        permalink: permalink
    });
  }
);
```

After we finish up getting all the highlight nodes we need to load up the highlight video page (it is a seperate page). When we load that we will grab the video ID and the excerpt for the main site page to alleviate the need for high bandwidth loading the main page of my site. Each sub page requires a sub request so we create an array of requests that we can then act on after they all come back.

 ``` javascript
 //After we get all the nodes for the videos we need to fetch the post page for the video url itself
_.forEach(highlightArray, function(highlight) {
    var vidProm = rp({
        uri: hostname + highlight.postUrl,
        transform: function(body) {
            return cheerio.load(body);
        }
    });
    videoPromises.push(vidProm);
});
```

When all video promises come back we grab those values mentioned. This is also where we use the `{replaceMe}` variable to string replace.

``` javascript
//after all the videos come back lets add it to the highlight array and then send it to GH
Promises.all(videoPromises).then(function(videos) {
    for (var i = 0; i < highlightArray.length; i++) {
      let videoHtml = iframeUrlTemplate.replace('{replaceMe}', videos[i]('video').attr('data-video-id'));
      let excerptText = videos[i]('.node .field-type-text-long p') .text()
      highlightArray[i].video = videoHtml;
      highlightArray[i].excerpt = excerptText; 
    }
    SendNewFilesToGitHubRepo(highlightArray);
});
```

Now that we have all the data for each post we can send the new files to the github repo. We do, however, need to make sure we don't **re**send the same file and duplicate the posts on GH so we will do a array diff.

First we will get all the files from the repo, technically only the subfolder where we are checking in the _posts/mnufc:

``` javascript
rp({
  qs: {
    access_token: context.secrets.GITHUB_ACCESS_TOKEN
  },
  headers: {
    'User-Agent': 'MN UFC auto blogger'
  },
  json: true,
  uri: `https://api.github.com/repos/Mutmatt/mutmatt.github.io/contents/_posts/mnufc/`
})
```

now that we have all the files we will diff the two arrays using lodash

``` javascript
//We don't want to recreate old files so we will diff the two arrays
let newPosts = _.differenceWith(allHighlights, response, function(mnufcValue, githubObject) {
  return mnufcValue.filename == githubObject.name;
});
```

Now this next part is all going to be wrapped in a `_.each(newPosts, function(post)` but will be ommitted for readibility

we format the file header for jekyll using the post data:

``` javascript
var postText = `---
title: ${post.title}
date: ${post.date}
permalink: ${post.permalink}
excerpt:${post.excerpt}
${postHeader}
${post.video}`;
```

Now we'll send all the new files to github. Based on github's api docs we need to base64 encode the content of the post. Since we are currently (in this contenxt) in a for each loop we will push the promises into an array to wait on later.

``` javascript
ghPromises.push(rp.put({
  qs: {
    access_token: context.secrets.GITHUB_ACCESS_TOKEN
  },
  headers: {
    'User-Agent': 'MN UFC auto blogger'
  },
  json: true,
  method: 'PUT',
  uri: `https://api.github.com/repos/Mutmatt/mutmatt.github.io/contents/_posts/mnufc/{$post.filename`,
  body: {
    path: '_posts/mnufc',
    message: post.title,
    content: Buffer.from(postText).toString('base64')
  }
})
```

That is the last step in the process. Now we just tell our webtask that we are done and return the new posts back. We don't use them currently but we could, theoretically do so.

``` javascript
//After all github files are created return the new posts
Promises.all(ghPromises).then(function () {
  cb(null, { newPosts });  
});
```

I set this webtask up as a cron to run once a day. That is probably excessive and could be done once every other day or once a week but it is a minimal task and should be fine daily.

The action of adding a new file to the repo triggers github pages to rebuild the site and brings the new file up to the site. ***#magix***.
