---
layout: default
title: Projects
subtitle: "Case studies — problem, diagnosis, approach, results, and learnings"
permalink: /ko/projects
---

## 하드웨어 인지형 추론 및 런타임 최적화

<div class="grid">
  {% assign hw_projects = site.projects_ko | where: "category", "hardware" | sort: "priority" %}
  {% for project in hw_projects %}
    <a class="project-tile" href="{{ project.url | relative_url }}">
      <div class="project-thumb">
        <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      </div>
      <div>
        <div class="project-title">{{ project.title }}</div>
        <div class="kpi">{{ project.summary | default: project.excerpt | default: project.content | markdownify | strip_html | normalize_whitespace | truncate: 180 }}</div>
      </div>
    </a>
  {% endfor %}
</div>

## 응용 ML 시스템 (보조 프로젝트)

<div class="grid">
  {% assign ml_projects = site.projects_ko | where: "category", "ml" | sort: "priority" %}
  {% for project in ml_projects %}
    <a class="project-tile" href="{{ project.url | relative_url }}">
      <div class="project-thumb">
        <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      </div>
      <div>
        <div class="project-title">{{ project.title }}</div>
        <div class="kpi">{{ project.summary | default: project.excerpt | default: project.content | markdownify | strip_html | normalize_whitespace | truncate: 180 }}</div>
      </div>
    </a>
  {% endfor %}
</div>
