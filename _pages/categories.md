---
# title: "Categories & Tags"
layout: categories
permalink: /categories/
---

## Categories

{% assign categories = site.categories | sort %}
{% for category in categories %}
  <h2 id="{{ category[0] | slugify }}">{{ category[0] | capitalize }}</h2>
  <ul>
    {% for post in category[1] %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%Y-%m-%d" }})
      </li>
    {% endfor %}
  </ul>
{% endfor %}

---

## Tags

{% assign tags = site.tags | sort %}
{% for tag in tags %}
  <h2 id="{{ tag[0] | slugify }}">{{ tag[0] | capitalize }}</h2>
  <ul>
    {% for post in tag[1] %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%Y-%m-%d" }})
      </li>
    {% endfor %}
  </ul>
{% endfor %}