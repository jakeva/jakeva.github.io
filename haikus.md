---
layout: page
title: Haikus
tagline: My haikus
group: navigation
---
{% include JB/setup %}

<style media="screen" type="text/css">

html, body {
    background: url(assets/grass.jpg) no-repeat center center fixed; 
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
}

</style>

<div class="well floatingBox" style="margin-top:25px">
 <ul class="haikus">
      {% for haiku in site.posts %}
      {% if haiku.category contains 'Haikus' %}
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
