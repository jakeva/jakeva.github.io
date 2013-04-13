---
layout: page
title: Haikus
tagline: My haikus
group: navigation
---
{% include JB/setup %}

<div class="floatingBox" style="margin-top:25px">
 <ul class="haikus">
      {% for haiku in site.posts %}
      {% if haiku.categories contains 'Haikus' %}
      <li>
          <h3>
              <a href="{{ haiku.url }}">
                  {{ haiku.title }}
              </a>
              <span class="haiku-date">
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
