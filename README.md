<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> <font size="-3">[{{ post.date }}]</font> 
    </li>
  {% endfor %}
</ul>
