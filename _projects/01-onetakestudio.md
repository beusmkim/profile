
---
layout: project
title: "OneTakeStudio – Hardware-Aware AI Inference System"
image: /assets/img/projects/onetakestudio_mainpage.png
published: false
---

## Overview
Hardware-aware AI video processing pipeline designed to maximize GPU efficiency under constrained VRAM environments.

## Technical Highlights

### CUDA-Based Inference Optimization
- Applied FP16 mixed precision (≈40% memory reduction)
- Reduced peak VRAM usage by ≈38%
- Improved average inference latency by ≈27%
- Controlled batch size dynamically based on runtime memory profiling
- Minimized GPU↔CPU tensor transfers
- Utilized CUDA streams for asynchronous execution

### Transformer Attention Optimization
- Analyzed memory-bound behavior in attention layers
- Reduced redundant graph execution
- Structured pipeline for future silicon-level benchmarking

### MSA-Based Compute Isolation
- Separated streaming (WebRTC) and AI inference workers
- Prevented compute blocking under concurrent load
- Reduced system blocking by ≈35%

---
Designed not as an application-layer service, but as a hardware-efficient AI execution architecture aligned with future AI silicon integration.
