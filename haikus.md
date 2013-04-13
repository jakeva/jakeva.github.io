---
layout: page
title: Haikus
tagline: My haikus
group: navigation
---
{% include JB/setup %}

<div class="floatingBox" style="margin-top:225px">
 <ul class="haikus">
      {% for haiku in site.haikus %}
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
     {% endfor %}
 </ul>
</div>
