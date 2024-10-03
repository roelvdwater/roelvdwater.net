---
layout: default
title: Tags
---

# Tags
This page contains a list of all the tags carried by the articles. Pick one you like and start crunching some of my words.
<ul class="tags all">
{% for tag in site.article_tags %}
	<li><a href="/tag/{{ tag.slug }}">{{ tag.name }}</a></li>
{% endfor %}