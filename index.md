{% for post in site.posts %}
  <h1><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h1>
  {{ post.excerpt }}
  {% if post.tags.size > 0 %}
  <footer class="article-footer">
    <ul class="tags">
      {% for tag in post.tags %}
        <li>{{ tag }}</li>
      {% endfor %}
    </ul>
  </footer>
  {% endif %}
{% endfor %}
