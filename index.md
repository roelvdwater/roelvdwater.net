{% for post in site.posts %}
  <h1><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h1>
  {% if post.tags.size > 0 %}
  <ul class="tags">
    {% for tag in post.tags %}
      <li>{{ tag }}</li>
    {% endfor %}
  </ul>
  {% endif %}
  {{ post.excerpt }}
  <p class="article-information"><span class="glyphicons glyphicons-clock"></span> 5 mins read</p>
{% endfor %}
