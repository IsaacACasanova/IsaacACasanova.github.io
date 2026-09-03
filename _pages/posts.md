---
layout: page
# `heading` instead of `title` on purpose: Menca's header lists every page that has a title
# in its nav, and this page only exists for the mono theme. Mono's layouts read `heading`.
heading: Posts
permalink: /posts/
---
<ul class="posts all">
{% for post in site.posts %}
  <li><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %Y" }}</time><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
