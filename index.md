---
layout: page
title: a (we)blog
tagline: Almost never updated
---
{% include JB/setup %}

<span>
I am a freelance Web, iOS and Mac OS X developer currently living in <a href="https://maps.google.com/maps/place?ftid=0x87523d9488d131ed:0x5b53b7a0484d31ca&q=Salt+Lake+City,+UT&hl=en&ie=UTF8&ll=40.760779,-111.891047&spn=0.00052,0.000687&t=h&z=11&vpsrc=0">Salt Lake City, Utah</a>. I love what I do, I started very young and as I got older, I began to branch out more and explored the world to the point that I felt ready to embrace geekdom professionally for the rest of my life. It took me a few years, but I came back. I'm continually fascinated by technology, I always have been. It was a lot of fun in the 80's on a monochrome Apple IIe, these days it's just ridiculous. Feel free to <a href="#" id="email_contact">get in touch</a>.
  <script type="text/javascript" >
      var _jvObfuscatedHREF0 = "mai";var _jvObfuscatedHREF1 = "lto";var _jvObfuscatedHREF2 = ":jak";var _jvObfuscatedHREF3 = "eva";var _jvObfuscatedHREF4 = "@gm";var _jvObfuscatedHREF5 = "ail";var _jvObfuscatedHREF6 = ".co";var _jvObfuscatedHREF7 = "m";var _jvObfuscatedHREF  = _jvObfuscatedHREF0+_jvObfuscatedHREF1+_jvObfuscatedHREF2+_jvObfuscatedHREF3+_jvObfuscatedHREF4+_jvObfuscatedHREF5+_jvObfuscatedHREF6+_jvObfuscatedHREF7;
      document.getElementById('email_contact').href = _jvObfuscatedHREF;
  </script>
   <img style="margin-top:5px; float: left; margin-right:10px; border:1px solid #000; width:150px;" src="assets/me.png"></img>
</span>

<div class="floatingBox" style="margin-top:225px">
 <ul class="posts">
      {% for post in site.posts %}
      <li>
          <h3>
              <a href="{{ post.url }}">
                  {{ post.title }}
              </a>
              <span class="post-date">
                  {{ post.date | date_to_string }}
             </span>
             <span>
             {{ p.url }}
             </span>
         </h3>
     </li>
     {% endfor %}
 </ul>
</div>
