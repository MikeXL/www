
### Insufficient facts always invite danger !!

<ul>
  {% for post in site.posts %}
    <li>
    <a href="{{ post.url }}">{{ post.title }}</a>  <font size="-2"><i>{{ post.date }}</i></font>
    </li>
  {% endfor %}
</ul>
