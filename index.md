---
layout: page
title: Irresistible Logic
tagline: Simplicity is the ultimate sophistication
---
{% include JB/setup %}

<span>
<h4 class="well" style="min-height:130px">
<div>
  <p style="display:inline">
    <img src="assets/jake.png" alt="Jake" style="margin:5px; float:left;">
    <p>I'm a software developer currently living in <a href="https://maps.google.com/maps/place?ftid=0x87523d9488d131ed:0x5b53b7a0484d31ca&amp;q=Salt+Lake+City,+UT&amp;hl=en&amp;ie=UTF8&amp;ll=40.760779,-111.891047&amp;spn=0.00052,0.000687&amp;t=h&amp;z=11&amp;vpsrc=0">Salt Lake City, Utah</a>. I wrote my first bit of code when I was 8 years old. I'm still writing software, and I've done a whole lot of other stuff too. It was a lot of fun when I started, these days it's just ridiculous. If you're looking for a disciplined developer with an eye for design, please <a id="email_contact">get in touch</a>.</p>
  </p>
</div>
</h4>
</span>

<div class="well floatingBox" style="float:left;">
 <ul class="posts">
      {% for post in site.posts %}
      {% if post.category contains 'Haikus' %}
      {% else %}
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
     {% endif %}
     {% endfor %}
 </ul>
</div>
