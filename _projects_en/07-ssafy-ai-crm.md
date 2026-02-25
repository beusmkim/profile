---
layout: project
title: "AI-based CRM Service Development (SSAFY)"
summary: "Defined segments from customer logs/purchase history, predicted conversion potential, and connected outputs to LLM-based scripts/messages."
period: "2025-2026"
role: "AI · Data"
stack: "Python, pandas, recommendation/classification modeling, LLM-assisted messaging"
image: /assets/img/projects/crm_mainpage.png
order: 90
featured: true
links:
  - label: "Repository"
    url: "https://github.com/BeusmKim/REPO"
---

## Overview
This project focused on turning customer data into execution-ready CRM actions.
Rather than stopping at descriptive analysis, the pipeline linked segmentation, conversion propensity, and message generation into one flow.

## Problem
- Customer logs existed, but targeting decisions were not connected to operational execution.
- Consultation and campaign messaging quality depended heavily on individual staff style.
- Teams needed a repeatable method to prioritize customers and standardize outreach.

## Approach
- Built segment definitions from customer logs and purchase history.
- Modeled conversion likelihood to rank actionable target groups.
- Connected ranked segments to LLM-assisted message/script generation for consistent execution.
- Organized the process as an operational workflow, not a one-time analytics report.

## Result
- Delivered a practical pipeline from data analysis to outreach execution.
- Enabled teams to prioritize high-conversion candidates with a standardized playbook.

## Limitation and Next Step
- Current version is project-scale and should be extended with live operational feedback loops.
- Next step is continuous calibration of segment and propensity outputs using real campaign outcomes.

## Screenshots
![CRM Main Page]({{ '/assets/img/projects/crm_mainpage.png' | relative_url }})
![CRM Customer Detail]({{ '/assets/img/projects/crm_customer_detail.png' | relative_url }})
![CRM Recommended]({{ '/assets/img/projects/crm_recommended.png' | relative_url }})
![CRM Recommended Scripts]({{ '/assets/img/projects/crm_recommended_scripts.png' | relative_url }})
![CRM Session Detail]({{ '/assets/img/projects/crm_session_detail.png' | relative_url }})
