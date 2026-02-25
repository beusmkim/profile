---
layout: default
title: Projects
subtitle: "Case studies — problem, diagnosis, approach, results, and learnings"
permalink: /ko/projects
---

## Hardware-aware inference & runtime optimization

<div class="grid">
  {% for project in site.projects_ko %}
    {% if project.path contains '01-ai-image-analysis' or project.path contains '02-onetakestudio' or project.path contains '03-aws-dc-siting' %}
    <a class="project-tile" href="{{ project.url | relative_url }}">
      <div class="project-thumb">
        <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      </div>
      <div>
        <div class="project-title">{{ project.title }}</div>
        <div class="kpi">{{ project.excerpt | strip_html | truncate: 180 }}</div>
      </div>
    </a>
    {% endif %}
  {% endfor %}
</div>

## Applied ML systems (lower priority)

<div class="grid">
  {% for project in site.projects_ko %}
    {% if project.path contains '07-ssafy-ai-crm' %}
    <a class="project-tile" href="{{ project.url | relative_url }}">
      <div class="project-thumb">
        <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      </div>
      <div>
        <div class="project-title">{{ project.title }}</div>
        <div class="kpi">{{ project.excerpt | strip_html | truncate: 180 }}</div>
      </div>
    </a>
    {% endif %}
  {% endfor %}
  {% for project in site.projects_ko %}
    {% if project.path contains '09-vqa-qwen' %}
    <a class="project-tile" href="{{ project.url | relative_url }}">
      <div class="project-thumb">
        <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      </div>
      <div>
        <div class="project-title">{{ project.title }}</div>
        <div class="kpi">{{ project.excerpt | strip_html | truncate: 180 }}</div>
      </div>
    </a>
    {% endif %}
  {% endfor %}
  {% for project in site.projects_ko %}
    {% if project.path contains '08-churn-ltv' %}
    <a class="project-tile" href="{{ project.url | relative_url }}">
      <div class="project-thumb">
        <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      </div>
      <div>
        <div class="project-title">{{ project.title }}</div>
        <div class="kpi">{{ project.excerpt | strip_html | truncate: 180 }}</div>
      </div>
    </a>
    {% endif %}
  {% endfor %}
  {% for project in site.projects_ko %}
    {% if project.path contains '10-cafe-ops-automation' %}
    <a class="project-tile" href="{{ project.url | relative_url }}">
      <div class="project-thumb">
        <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      </div>
      <div>
        <div class="project-title">{{ project.title }}</div>
        <div class="kpi">{{ project.excerpt | strip_html | truncate: 180 }}</div>
      </div>
    </a>
    {% endif %}
  {% endfor %}
</div>
