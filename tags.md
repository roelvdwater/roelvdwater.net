{% for t in site.tags %}
    {% if t.Name == page.tag %}
        {% for post in t.posts reverse %}
     	    {{ post.title }}
            <hr>
        {% endfor %}
    {% endif %}
{% endfor %}
