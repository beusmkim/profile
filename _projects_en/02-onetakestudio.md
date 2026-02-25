---
layout: project
title: "OneTakeStudio — Compute-Isolated AI Inference System"
image: /assets/img/projects/onetakestudio_mainpage.png
---

## Overview
A real-time content pipeline where compute-heavy inference is isolated from the streaming layer to maintain latency stability. The core engineering focus was system architecture: preventing inference workloads from degrading real-time services.

## Problem
When inference and streaming ran in a tightly coupled path:
- GPU contention and blocking increased under concurrent requests
- Real-time streaming quality degraded during heavy inference
- Scaling inference capacity risked destabilizing the interactive path

## Diagnosis
The primary bottleneck was not a single model component, but **resource contention**:
- Inference workloads competed with streaming tasks for CPU/GPU time
- Blocking cascaded when one stage stalled (backpressure)
- Lack of isolation made tuning or scaling fragile

## Approach
### Compute isolation architecture (MSA)
- Separated streaming (WebRTC layer) from inference workers
- Routed inference via worker orchestration to prevent contention

### Hardware-aware inference path
- Applied FP16 in inference workers to reduce VRAM pressure
- Designed workers so GPU-intensive tasks do not block I/O and streaming

### Scalability
- Enabled horizontal scaling by adding inference workers independently
- Preserved streaming latency by design (isolation first, optimization second)

## Result
- Blocking reduction under concurrency: **~35%**
- Improved throughput stability without harming the streaming path
- Cleaner profiling and optimization surface (workers can be tuned independently)

## Screenshots
![OneTakeStudio Main Page]({{ '/assets/img/projects/onetakestudio_mainpage.png' | relative_url }})
![OneTakeStudio Generate Shorts]({{ '/assets/img/projects/onetakestudio_generate_shorts.png' | relative_url }})
![OneTakeStudio Shorts Output]({{ '/assets/img/projects/onetakestudio_shorts_output.png' | relative_url }})

## Key insight
In real-time systems, architecture is a first-order performance lever. Compute isolation creates a stable baseline where model-level optimizations (precision, kernels) can produce reliable gains without causing regressions in latency-sensitive services.
