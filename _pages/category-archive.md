---
permalink: /posts/
layout: archive
author_profile: true
classes: wide
---

<ul class="taxonomy__index">
  {% assign categories_max = 0 %}
  {% for category in site.categories %}
    {% if category[1].size > categories_max %}
      {% assign categories_max = category[1].size %}
    {% endif %}
  {% endfor %}
  {% for i in (1..categories_max) reversed %}
    {% for category in site.categories %}
      {% if category[1].size == i %}
        <li>
          <a href="#{{ category[0] | slugify }}">
            <strong>{{ category[0] }}</strong> <span class="taxonomy__count">{{ i }}</span>
          </a>
        </li>
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>

{% assign entries_layout = page.entries_layout | default: 'list' %}
{% for category in site.categories %}
  <section id="{{ category[0] | slugify }}" class="taxonomy__section">
    <h2 class="archive__subtitle">{{ category[0] }}</h2>
    <div class="entries-{{ entries_layout }}">
      {% for post in category.last %}
        {% include archive-single.html type=entries_layout %}
      {% endfor %}
    </div>
    <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'back to top' }} &uarr;</a>
  </section>
{% endfor %}