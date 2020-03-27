---
layout: page
title: Blog
---
{% include JB/setup %}
<div class="row">
  <div class="span8">
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
  <div class="span4">
    <h2>About Me</h2>
    <p>I'm Jake. I live in Salt Lake City, and I do various things with computers. I read, cook, go outside, and stay inside. I mostly post here from my phone using some custom shortcuts and python scripts.</p>
  </div>
</div>
