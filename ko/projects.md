---
layout: default
title: Projects
subtitle: "케이스 스터디 - 문제, 접근, 결과, 학습"
permalink: /ko/projects
---

<div class="grid">
{% assign allp = site.projects | where_exp: "p", "p.published != false" | sort: "order" %}
{% for p in allp %}
  <a class="project-tile" href="{{ p.url | relative_url }}">
    {% if p.image %}
      <div class="project-thumb"><img src="{{ p.image | relative_url }}" alt="{{ p.title }} thumbnail" /></div>
    {% else %}
      <div class="project-thumb placeholder">No image</div>
    {% endif %}
    <div>
      <div class="project-title">{{ p.title }}</div>
      <div class="kpi">{{ p.summary }}</div>
      <div class="kpi">Stack: {{ p.stack }}</div>
    </div>
  </a>
{% endfor %}
</div>
