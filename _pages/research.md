---
layout: page
title: "Research"
permalink: /research/
---

{% assign cats = site.research_category %}
{% assign order = "books,manuscripts,working_papers,works_in_progress,conferences" | split: "," %}

{% for key in order %}
  {% assign k = key | strip %}
  {% assign heading = cats[k].title %}
  {% assign items = site.research | where: "category", k | sort: "date" | reverse %}

  {% if items and items.size > 0 %}
  <h2>{{ heading }}</h2>
  <ul class="list-unstyled">
    {% for p in items %}
      <li style="margin-bottom:1.1rem;">
        <strong><a href="{{ p.url | relative_url }}">{{ p.title }}</a></strong><br/>
        {% if p.venue %}<em>{{ p.venue }}</em>{% endif %}
        {% if p.date %}{% if p.venue %} · {% endif %}{{ p.date | date: "%Y" }}{% endif %}<br/>
        {% if p.excerpt %}<span>{{ p.excerpt }}</span><br/>{% endif %}
        {% if p.paperurl %}<a href="{{ p.paperurl }}">PDF</a>{% endif %}
        {% if p.bibtexurl %}{% if p.paperurl %} · {% endif %}<a href="{{ p.bibtexurl }}">BibTeX</a>{% endif %}
      </li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}
