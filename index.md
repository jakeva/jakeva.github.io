---
layout: page
title: My Blog
tagline: Inessential Ramblings & Banal Platitudes
---
{% include JB/setup %}

<div class="floatingBox" style="float:left;">
  <ul class="posts">
      {% for post in site.posts %}
      {% if post.category contains 'Haikus' %}
      {% else %}
      <li>
          <h3>
              <a href="{{ post.url }}">
                  {{ post.title }}
              </a>
              <span class="post-date" style="float: right; padding-left: 24px;">
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
