---
layout: default
title: Projects
subtitle: "Case studies — problem, diagnosis, approach, results, and learnings"
permalink: /projects
---

<div class="card">
  <h2 style="margin-top:0">How to read these</h2>
  <p style="margin:0">
    Each project is written in a consistent structure: <strong>Problem → Diagnosis → Approach → Result → Insight</strong>.
    The first section prioritizes hardware-aware inference and runtime optimization work.
  </p>
</div>

## Hardware-aware inference & runtime optimization

<div class="grid">
  {% for project in site.projects_en %}
    {% if project.path contains '01-ai-image-analysis' or project.path contains '02-onetakestudio' or project.path contains '03-aws-dc-siting' %}
    <a class="project-card" href="{{ project.url | relative_url }}">
      <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      <div class="project-card-body">
        <h3>{{ project.title }}</h3>
        <p>{{ project.excerpt | strip_html | truncate: 180 }}</p>
      </div>
    </a>
    {% endif %}
  {% endfor %}
</div>

## Applied ML systems (lower priority)

<div class="grid">
  {% for project in site.projects_en %}
    {% if project.path contains '07-ssafy-ai-crm' or project.path contains '08-churn-ltv' or project.path contains '09-vqa-qwen' or project.path contains '10-cafe-ops-automation' %}
    <a class="project-card" href="{{ project.url | relative_url }}">
      <img src="{{ project.image | relative_url }}" alt="{{ project.title }}"/>
      <div class="project-card-body">
        <h3>{{ project.title }}</h3>
        <p>{{ project.excerpt | strip_html | truncate: 180 }}</p>
      </div>
    </a>
    {% endif %}
  {% endfor %}
</div>
