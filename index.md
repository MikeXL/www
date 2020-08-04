---
layout: default
---
{% for post in site.posts %}	
<ol>
    <small>{{ post.date | date_to_string: "ordinal" }} </small> | {{ post.title }} . {{ post.category }} .
</ol>
{% endfor %}	
