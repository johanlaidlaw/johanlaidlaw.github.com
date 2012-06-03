---
layout: page
title: Johan Laidlaw
---
{% include JB/setup %}

{% for post in site.posts %}
<div class="post">
    <h2><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2>
    <p>
      <span class="date">{{ post.date | date_to_string }}</span>
    </p>
    <p>
      {{ post.content | strip_html | truncate: 200 }}
    </p>
  
</div>
{% endfor %}