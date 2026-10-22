---
layout: page
title: People
permalink: /people/
description: The current and past members of my group
nav: true
nav_order: 3
---

<style>
  .people-list {
    margin-left: 0px;
    margin-right: 50px;
  }

  .person-entry {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    margin: 0 0 1.5rem;
    margin-left: 50px;
  }

  .person-entry__photo {
    display: block;
    flex: 0 0 100px;
    width: 100px;
    height: 100px;
    object-fit: cover;
    object-position: center;
    border-radius: 4px;
  }

  .person-entry__details {
    min-width: 0;
    flex: 1;
  }

  .person-entry__details ul {
    margin-top: 0.35rem;
    margin-bottom: 0;
    padding-left: 1.2rem;
  }

  @media (max-width: 600px) {
    .people-list {
      margin-left: 0;
      margin-right: 0;
    }

    .person-entry {
      gap: 10px;
    }
  }
</style>

{% assign people_sections = "phd|PhD students,postdoc|Postdoctoral researchers,master students|Master's students,undergraduates|Undergraduate students" | split: "," %}
<div class="people-list">
{% for section in people_sections %}
  {% assign parts = section | split: "|" %}
  {% assign key = parts[0] %}
  {% assign heading = parts[1] %}
  {% assign people = site.data.generated_people[key] %}
  {% assign current_people = people | where_exp: "person", "person.is_alumni == false" %}
  {% assign alumni = people | where_exp: "person", "person.is_alumni == true" %}

  <h2>{{ heading }}</h2>
  
  {% if current_people.size > 0 %}
    <h4 style="margin-left: 50px;">Current members</h4>
    {% for person in current_people %}
      {% assign picture_src = person.picture %}
      {% if picture_src == blank %}
        {% assign picture_src = "/assets/img/people/someone.png" | relative_url %}
      {% else %}
        {% unless picture_src contains "://" %}
          {% assign picture_src = picture_src | relative_url %}
        {% endunless %}
      {% endif %}
      <div class="person-entry">
        <img src="{{ picture_src | escape }}" alt="Photo of {{ person.name | escape }}" class="person-entry__photo" loading="lazy">
        <div class="person-entry__details">
          <strong>{% if person.website != blank %}<a href="{{ person.website | escape }}" target="_blank" rel="noopener noreferrer">{% endif %}{{ person.name | escape }}{% if person.website != blank %}</a>{% endif %}</strong>
          <ul>
            {% if person.department != blank %}<li>Department: {{ person.department | escape }}</li>{% endif %}
            {% if person.graduation_year != blank %}<li>{% if key == "postdoc" %}Period{% else %}Planned graduation year{% endif %}: {{ person.graduation_year | escape }}</li>{% endif %}
            {% if person.coadvisor != blank %}<li>Co-advised with {{ person.coadvisor | escape }}</li>{% endif %}
          </ul>
        </div>
      </div>
    {% endfor %}
  {% else %}
    <p  style="margin-left: 50px;"><em>No current members listed.</em></p>
  {% endif %}
  
  {% if alumni.size > 0 %}
    <h4 style="margin-left: 50px;">Alumni</h4>
    {% for person in alumni %}
      {% assign picture_src = person.picture %}
      {% if picture_src == blank %}
        {% assign picture_src = "/assets/img/people/someone.png" | relative_url %}
      {% else %}
        {% unless picture_src contains "://" %}
          {% assign picture_src = picture_src | relative_url %}
        {% endunless %}
      {% endif %}
      <div class="person-entry">
        <img src="{{ picture_src | escape }}" alt="Photo of {{ person.name | escape }}" class="person-entry__photo" loading="lazy">
        <div class="person-entry__details">
          <strong>{% if person.website != blank %}<a href="{{ person.website | escape }}" target="_blank" rel="noopener noreferrer">{% endif %}{{ person.name | escape }}{% if person.website != blank %}</a>{% endif %}</strong>
          <ul>
            {% if person.graduation_year != blank %}<li>{% if key == "postdoc" %}Period{% else %}Graduated in{% endif %}: {{ person.graduation_year | escape }}</li>{% endif %}
            {% if person.department != blank %}<li>Department: {{ person.department | escape }}</li>{% endif %}
            {% if person.coadvisor != blank %}<li>Co-advised with {{ person.coadvisor | escape }}</li>{% endif %}
            {% if person.now_working_at != blank %}<li>Now working at {{ person.now_working_at | escape }}</li>{% endif %}
          </ul>
        </div>
      </div>
    {% endfor %}
  {% endif %}
{% endfor %}
</div>
