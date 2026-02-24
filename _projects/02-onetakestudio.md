---
layout: project
title: "OneTakeStudio – Distributed AI Inference & Compute Isolation"
image: /assets/img/projects/onetakestudio_mainpage.png
---

## Overview
A distributed AI inference system designed to isolate compute-heavy workloads and stabilize GPU utilization.

## Architectural Focus

### Compute Isolation (MSA)
- Separated streaming layer from inference workers
- Reduced GPU contention
- Achieved ~35% reduction in blocking under concurrent workloads

### Hardware-Aware Inference
- Applied FP16 precision to reduce VRAM pressure
- Structured inference path for hardware-aligned execution
- Designed system for scalable worker-based expansion

## Engineering Value
Emphasizes runtime stability, GPU resource orchestration, and inference scalability rather than product features.

## Screenshots
![OneTakeStudio Main Page]({{ '/assets/img/projects/onetakestudio_mainpage.png' | relative_url }})
![OneTakeStudio Generate Shorts]({{ '/assets/img/projects/onetakestudio_generate_shorts.png' | relative_url }})
![OneTakeStudio Shorts Output]({{ '/assets/img/projects/onetakestudio_shorts_output.png' | relative_url }})
