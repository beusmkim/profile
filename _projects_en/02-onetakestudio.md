---
layout: project
title: "OneTakeStudio — Compute-Isolated AI Inference System"
image: /assets/img/projects/onetakestudio_mainpage.png
---

## Overview

A real-time AI pipeline redesigned to isolate compute-heavy inference from latency-sensitive streaming.

---

## Problem

Tightly coupled streaming and inference execution caused:

- GPU contention under concurrent requests
- Latency spikes propagating to streaming
- Backpressure cascading across execution stages

The issue was architectural, not algorithmic.

---

## Measurement Context

- Concurrent inference requests
- GPU utilization monitoring
- Frame drop correlation analysis

Observed:
- GPU utilization peaks aligned with streaming FPS degradation
- Blocking events correlated with inference bursts

---

## Diagnosis

Resource contention between streaming I/O and inference workloads caused unstable latency.

---

## Approach

### Compute Isolation (MSA)
- Separated streaming and inference services
- Introduced worker-based orchestration

### Hardware-Aware Worker Design
- Applied FP16 inside workers
- Prevented GPU-bound tasks from blocking I/O threads

### Scalability
- Enabled horizontal scaling of inference workers
- Preserved streaming latency during scaling

---

## Result

- Blocking reduced by ~35%
- Latency variance stabilized
- Clear profiling boundary for further optimization

---

## Insight

In real-time AI systems, architecture determines performance ceilings.  
Isolation of critical paths mirrors hardware-software co-design principles.