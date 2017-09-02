
### Insufficient facts always invite danger !!

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> {{ post.date }}
    </li>
  {% endfor %}
</ul>
