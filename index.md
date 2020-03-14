---
layout: page
title: Jake Van Alstyne
tagline: Software Developer
---
{% include JB/setup %}

<div>
  <p style="display:inline">
    <img src="assets/jake.png" alt="Jake" style="margin:5px; float:left; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.8);">
    <p>I make things, mostly software things.</p>
  </p>
</div>

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
