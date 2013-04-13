---
layout: page
title: Haikus
tagline: My haikus
group: navigation
---
{% include JB/setup %}
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
