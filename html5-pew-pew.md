---
title: HTML5 Pew-Pew
date: 2014-07-31T14:54:06+00:00
excerpt: "Play some galaga, have a good time, check out the code. It's all open source!"
layout: page
---
<link href="https://cdn.rawgit.com/Mutmatt/Pew-Pew/v1.0/css/bootstrap-responsive.min.css" type="spreadsheet" />

<link href='https://fonts.googleapis.com/css?family=Iceland' rel='stylesheet' type='text/css' />

<div class="footer" align="center">
  <h1 class="text-info">
    Key Buttons
  </h1>
  
  <p>
    <b style="color:red;">Arrow Keys or Mouse</b>: Move <br /> &#8216;<b style="color:red;">Space</b>&#8216;: Shoot <br /> &#8216;<b style="color:red;">z</b>&#8216;: Bomb <br /> &#8216;<b style="color:red;">x</b>&#8216;: Shotgun <br /> &#8216;<b style="color:red;">c</b>&#8216;: Shield <br /> &#8216;<b style="color:red;">Shift</b>&#8216; + &#8216;<b style="color:red;">Arrow</b>&#8216;: Bullet Control<br />
  </p>
</div><canvas id="galaga_canvas" width="400" height="400" style="background-color:black;" tabindex='1'></canvas>


<div id="img_source" style="display:none;">
  <img id="bad1" src="https://mutmatt.github.io/images/pew-pew/bad2.png?w=750" data-recalc-dims="1" /> <img id="bad2" src="https://mutmatt.github.io/images/pew-pew/bad3.png?w=750" data-recalc-dims="1" /> <img id="bad3" src="https://mutmatt.github.io/images/pew-pew/bad1.png?w=750" data-recalc-dims="1" /> <img id="good" src="https://mutmatt.github.io/images/pew-pew/good.png?w=750" data-recalc-dims="1" /> <img id="suri" src="https://mutmatt.github.io/images/pew-pew/suri.png?w=750" data-recalc-dims="1" /> <img id="vim" src="https://mutmatt.github.io/images/pew-pew/vim.png?w=750" data-recalc-dims="1" /> <img id="laser" src="https://mutmatt.github.io/images/pew-pew/laser11.png?resize=40%2C24"  data-recalc-dims="1" /> <img id="boss" src="https://mutmatt.github.io/images/pew-pew/bc.png?resize=90%2C70"  data-recalc-dims="1" /> <img id="explosion" src="https://mutmatt.github.io/images/pew-pew/explosion1.png?w=750" data-recalc-dims="1" />
</div><audio id="sound0"> <source src="https://mutmatt.github.io/images/pew-pew/galaga0.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga0.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound1"> <source src="https://mutmatt.github.io/images/pew-pew/galaga1.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga1.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound2"> <source src="https://mutmatt.github.io/images/pew-pew/galaga2.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga2.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound3"> <source src="https://mutmatt.github.io/images/pew-pew/galaga3.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga3.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound4"> <source src="https://mutmatt.github.io/images/pew-pew/galaga4.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga4.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound5"> <source src="https://mutmatt.github.io/images/pew-pew/galaga5.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga5.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound6"> <source src="https://mutmatt.github.io/images/pew-pew/galaga6.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga6.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound7"> <source src="https://mutmatt.github.io/images/pew-pew/galaga7.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga7.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound8"> <source src="https://mutmatt.github.io/images/pew-pew/galaga8.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga8.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound9"> <source src="https://mutmatt.github.io/images/pew-pew/galaga9.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga9.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound11"> <source src="https://mutmatt.github.io/images/pew-pew/galaga11.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga11.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound12"> <source src="https://mutmatt.github.io/images/pew-pew/galaga12.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga12.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound13"> <source src="https://mutmatt.github.io/images/pew-pew/galaga13.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga13.wav"></source> Your browser doesn&#8217;t support our audio files </audio> <audio id="sound14"> <source src="https://mutmatt.github.io/images/pew-pew/galaga14.mp3"></source> <source src="https://mutmatt.github.io/images/pew-pew/galaga14.wav"></source> Your browser doesn&#8217;t support our audio files </audio> This project is also available on 

<a href="https://github.com/Mutmatt/Pew-Pew" title="HTML5 Galaga" rel="external" target="_blank">GitHub:Mutmatt/Pew-Pew</a>  


  
Special thanks go out to:
  
Weapon Upgrades: <a href="https://plus.google.com/111302679105358219806/about" target="_blank">SeongJae Park</a>
  
Sound Effect: <a href="https://plus.google.com/106958385030616827332/about" target="_blank">Haebin Yoon</a>
  
Recover The Original Motion: <a href="https://plus.google.com/111516089306509884557/about" target="_blank">JongYoon Lim</a>
  
Boss Stage: <a href="https://plus.google.com/107621265594457706915/about" target="_blank">Lee WonJae</a>