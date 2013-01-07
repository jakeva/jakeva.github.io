---
layout: page
title: Blog
tagline: Almost never updated
---
{% include JB/setup %}

<span>
I am a freelance Web, iOS and Mac OS X developer currently living in <a href="https://maps.google.com/maps/place?ftid=0x87523d9488d131ed:0x5b53b7a0484d31ca&q=Salt+Lake+City,+UT&hl=en&ie=UTF8&ll=40.760779,-111.891047&spn=0.00052,0.000687&t=h&z=11&vpsrc=0">Salt Lake City, Utah</a>. I really love what I do. I'm continually fascinated by technology, I started on an Apple IIe back in the 80's and today I'm on a 15" Macbook Pro. The professional world finds me working in Windows (Visual Studio) from time to time, but if you want to know... no, I don't like it. Feel free to

              <a href="#" id="email_contact">contact</a> me.
  <script type="text/javascript" >
      var _jvObfuscatedHREF0 = "mai";var _jvObfuscatedHREF1 = "lto";var _jvObfuscatedHREF2 = ":jak";var _jvObfuscatedHREF3 = "eva";var _jvObfuscatedHREF4 = "@gm";var _jvObfuscatedHREF5 = "ail";var _jvObfuscatedHREF6 = ".co";var _jvObfuscatedHREF7 = "m";var _jvObfuscatedHREF  = _jvObfuscatedHREF0+_jvObfuscatedHREF1+_jvObfuscatedHREF2+_jvObfuscatedHREF3+_jvObfuscatedHREF4+_jvObfuscatedHREF5+_jvObfuscatedHREF6+_jvObfuscatedHREF7;
      document.getElementById('email_contact').href = _jvObfuscatedHREF;
  </script>
   <img style="margin-top:5px; float: left; margin-right:10px; border:1px solid #000; width:150px;" src="assets/me.png"></img>
</span>

<div style="margin-top:225px">
 <ul class="posts floatingBox">
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
