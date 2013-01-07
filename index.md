---
layout: page
title: Blog
tagline: Words and stuff
---
{% include JB/setup %}

I am a freelance Web, iOS and Mac OS X developer currently living in Salt Lake City.


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

