---
layout: project
title: "OneTakeStudio – Distributed AI Inference Architecture"
image: /assets/img/projects/onetakestudio_mainpage.png
---

## Overview
Real-time video AI processing system designed with compute isolation and hardware-aware inference scaling.

## Architecture Highlights

### Compute Isolation (MSA)
- Separated streaming (WebRTC) and AI inference workers
- Prevented GPU contention
- ~35% reduction in system blocking

### Transformer Inference Optimization
- Applied FP16 mixed precision
- Reduced VRAM pressure
- Stabilized throughput under concurrent requests

### Scalability
- Designed worker-based horizontal scaling
- Structured for future hardware accelerator integration

Built not as a media tool, but as a hardware-efficient distributed AI execution system.
