---
layout: page
title: Blog
---
{% include JB/setup %}

<div class="floatingBox">
  <h3><a href="/posts">
    Posts
  </a></h3>
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
  <h3><a href="/haikus">
    Haikus
  </a></h3>
  <ul class="posts">
    {% for haiku in site.posts %}
    {% if haiku.category contains 'Haikus' %}
    <li>
      <h3>
        <a href="{{ haiku.url }}">
          {{ haiku.title }}
        </a>
        <span class="post-date">
          {{ haiku.date | date_to_string }}
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
