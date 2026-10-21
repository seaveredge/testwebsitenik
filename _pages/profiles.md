---
layout: page
title: People
permalink: /people/
description: The current and past members of my group
nav: true
nav_order: 3
---

{% assign people_sections = "phd|PhD students,postdoc|Postdoctoral researchers,master students|Master's students,undergraduates|Undergraduate students" | split: "," %}
{% for section in people_sections %}
  {% assign parts = section | split: "|" %}
  {% assign key = parts[0] %}
  {% assign heading = parts[1] %}
  {% assign people = site.data.generated_people[key] %}
  {% assign current_people = people | where_exp: "person", "person.is_alumni == false" %}
  {% assign alumni = people | where_exp: "person", "person.is_alumni == true" %}

### {{ heading }}

{% if current_people.size > 0 %}
#### Current members
  {% for person in current_people %}
<div class="row mb-4 align-items-start">
  {% if person.picture != "" %}{% assign picture_src = person.picture %}{% unless person.picture contains "://" %}{% assign picture_src = person.picture | relative_url %}{% endunless %}<div class="col-sm-3 col-md-2 mb-2"><img src="{{ picture_src | escape }}" alt="Photo of {{ person.name | escape }}" class="img-fluid rounded" loading="lazy" style="max-width: 50px;"></div>{% endif %}
  <div class="col"><strong>{% if person.website != blank %}<a href="{{ person.website | escape }}" target="_blank" rel="noopener noreferrer">{% endif %}{{ person.name | escape }}{% if person.website != blank %}</a>{% endif %}</strong><ul>
    {% if person.department != "" %}<li>{{ person.department | escape }}</li>{% endif %}
    {% if person.graduation_year != "" %}<li>{% if key == "postdoc" %}Period{% else %}Planned graduation year{% endif %}: {{ person.graduation_year | escape }}</li>{% endif %}
    {% if person.coadvisor != "" %}<li>Co-advised with {{ person.coadvisor | escape }}</li>{% endif %}
  </ul></div>
</div>
  {% endfor %}
{% else %}
_No current members listed._
{% endif %}

{% if alumni.size > 0 %}
#### Alumni
{% for person in alumni %}
<div class="row mb-3 align-items-start">
  {% if person.picture != "" %}{% assign picture_src = person.picture %}{% unless person.picture contains "://" %}{% assign picture_src = person.picture | relative_url %}{% endunless %}<div class="col-sm-3 col-md-2 mb-2"><img src="{{ picture_src | escape }}" alt="Photo of {{ person.name | escape }}" class="img-fluid rounded" loading="lazy" style="max-width: 50px;"></div>{% endif %}
  <div class="col"><strong>{{ person.name | escape }}</strong>{% if person.graduation_year != "" %} ({{ person.graduation_year | escape }}){% endif %}{% if person.website != blank %} · <a href="{{ person.website | escape }}" target="_blank" rel="noopener noreferrer">Personal website</a>{% endif %}<ul>
    {% if person.department != "" %}<li>{{ person.department | escape }}</li>{% endif %}
    {% if person.coadvisor != "" %}<li>Co-advised with {{ person.coadvisor | escape }}</li>{% endif %}
    {% if person.now_working_at != blank %}<li>Now working at {{ person.now_working_at | escape }}</li>{% endif %}
  </ul></div>
</div>
{% endfor %}
{% endif %}
{% endfor %}
