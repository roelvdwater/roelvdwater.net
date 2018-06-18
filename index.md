{% for post in site.posts %}
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <ul class="tags">
    {% for tag in post.tags %}
      <li>{% tag %}</li>
    {% endfor %}
  </ul>
  {{ post.excerpt }}
{% endfor %}
