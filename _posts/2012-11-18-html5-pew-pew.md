---
id: 229
title: HTML5 Pew-Pew (Galaga remake)!!!
date: 2012-11-18T08:59:15+00:00
layout: post
guid: http://matterickson.me/?p=229
permalink: /html5-pew-pew/
enclosure:
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga0.mp3
        9612
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga0.wav
        21240
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga1.mp3
        7104
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga1.wav
        14106
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga2.mp3
        6268
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga2.wav
        12464
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga3.mp3
        6268
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga3.wav
        12174
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga4.mp3
        48900
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga4.wav
        130248
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga5.mp3
        6268
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga5.wav
        11768
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga6.mp3
        6268
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga6.wav
        12648
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga7.mp3
        21732
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga7.wav
        54596
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga8.mp3
        53915
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga8.wav
        144086
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga9.mp3
        51826
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga9.wav
        138092
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga11.mp3
        9221
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga11.wav
        96712
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga12.mp3
        9221
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga12.wav
        96712
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga13.mp3
        9221
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga13.wav
        96712
        audio/wav
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga14.mp3
        8069
        audio/mpeg
        
  - |
    |
        http://matterickson.me/wp-content/uploads/2013/03/galaga14.wav
        43792
        audio/wav
        
spacious_page_layout:
  - default_layout
categories:
  - Development
  - Featured
  - HTML5/CSS3
  - Web
tags:
  - galaga
  - game
  - html5
---
<link href="https://rawgithub.com/Mutmatt/Pew-Pew/v1.0/css/bootstrap-responsive.min.css" type="spreadsheet" />

<link href='http://fonts.googleapis.com/css?family=Iceland' rel='stylesheet' type='text/css' />

<div class="footer" align="center">
  <h1 class="text-info">
    Key Buttons
  </h1>
  
  <p>
    <b style="color:red;">Arrow Keys or Mouse</b>: Move <br /> &#8216;<b style="color:red;">Space</b>&#8216;: Shoot <br /> &#8216;<b style="color:red;">z</b>&#8216;: Bomb <br /> &#8216;<b style="color:red;">x</b>&#8216;: Shotgun <br /> &#8216;<b style="color:red;">c</b>&#8216;: Shield <br /> &#8216;<b style="color:red;">Shift</b>&#8216; + &#8216;<b style="color:red;">Arrow</b>&#8216;: Bullet Control<br />
  </p>
</div><canvas id="galaga_canvas" width="400" height="400" style="background-color:black;" tabindex='1'></canvas>



    


<div id="img_source" style="display:none;">
  <img id="bad1" src="http://i2.wp.com/matterickson.me/wp-content/uploads/2013/03/bad2.png?w=750" data-recalc-dims="1" /> <img id="bad2" src="http://i2.wp.com/matterickson.me/wp-content/uploads/2013/03/bad3.png?w=750" data-recalc-dims="1" /> <img id="bad3" src="http://i0.wp.com/matterickson.me/wp-content/uploads/2013/03/bad1.png?w=750" data-recalc-dims="1" /> <img id="good" src="http://i0.wp.com/matterickson.me/wp-content/uploads/2013/03/good.png?w=750" data-recalc-dims="1" /> <img id="suri" src="http://i1.wp.com/matterickson.me/wp-content/uploads/2013/03/suri.png?w=750" data-recalc-dims="1" /> <img id="vim" src="http://i2.wp.com/matterickson.me/wp-content/uploads/2013/03/vim.png?w=750" data-recalc-dims="1" /> <img id="laser" src="http://i0.wp.com/matterickson.me/wp-content/uploads/2013/03/laser11.png?resize=40%2C24"  data-recalc-dims="1" /> <img id="boss" src="http://i1.wp.com/matterickson.me/wp-content/uploads/2013/03/bc.png?resize=90%2C70"  data-recalc-dims="1" /> <img id="explosion" src="http://i2.wp.com/matterickson.me/wp-content/uploads/2013/03/explosion1.png?w=750" data-recalc-dims="1" />
</div><audio id="sound0"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga0.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga0.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound1"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga1.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga1.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound2"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga2.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga2.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound3"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga3.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga3.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound4"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga4.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga4.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound5"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga5.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga5.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound6"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga6.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga6.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound7"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga7.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga7.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound8"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga8.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga8.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound9"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga9.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga9.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound11"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga11.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga11.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound12"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga12.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga12.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound13"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga13.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga13.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound14"> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga14.mp3"></source> <source src="http://matterickson.me/wp-content/uploads/2013/03/galaga14.wav"></source> Your browser doesn&#8217;t support our audio files </audio> This project is also available on 

<a href="https://github.com/Mutmatt/Pew-Pew" title="HTML5 Galaga" rel="external" target="_blank">GitHub:Mutmatt/Pew-Pew</a>  


  
Special thanks go out to:
  
Weapon Upgrades: <a href="https://plus.google.com/111302679105358219806/about" target="_blank">SeongJae Park</a>
  
Sound Effect: <a href="https://plus.google.com/106958385030616827332/about" target="_blank">Haebin Yoon</a>
  
Recover The Original Motion: <a href="https://plus.google.com/111516089306509884557/about" target="_blank">JongYoon Lim</a>
  
Boss Stage: <a href="https://plus.google.com/107621265594457706915/about" target="_blank">Lee WonJae</a>