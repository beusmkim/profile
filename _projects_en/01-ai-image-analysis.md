---
layout: project
title: "AI Image Analysis — Memory-Bound Inference Optimization"
image: /assets/img/projects/aiimage0.png
---

## Overview
This project focuses on improving inference stability and efficiency for transformer-based image analysis under constrained GPU resources. The goal was not to increase model size, but to reduce VRAM pressure and mitigate bandwidth-driven latency spikes.

## Problem
Data augmentation and hyperparameter tuning improved model quality up to a point, but deployment performance remained unstable:
- Peak VRAM spikes caused occasional out-of-memory failures
- Latency variance increased under concurrency
- Additional training did not address runtime bottlenecks

## Diagnosis
Profiling and symptom-driven investigation suggested the workload was **memory-bandwidth bound**, especially around attention-heavy execution:
- High Q/K/V tensor movement increased global memory pressure
- Latency rose before compute utilization saturated
- Memory allocation patterns contributed to fragmentation and VRAM spikes

## Approach
### Mixed precision deployment (FP16)
- Converted FP32 inference path to FP16 where safe
- Reduced activation and tensor footprint to lower bandwidth pressure

### Quantization exploration (INT8)
- Compared FP16 vs INT8 trade-offs on representative inputs
- Prioritized latency improvement while monitoring output quality stability

### CUDA-aware runtime improvements
- Applied asynchronous execution concepts (CUDA streams)
- Reduced unnecessary CPU↔GPU tensor transfers and redundant copies
- Mitigated fragmentation by improving allocation and reuse patterns

## Result
- Peak VRAM reduction: **~38–40%** (FP16 deployment)
- Inference latency improvement: **~22%** (precision/quantization strategy exploration)
- Improved stability under constrained GPUs (reduced OOM incidence and latency variance)

## Screenshots
![AI Image Analysis 0]({{ '/assets/img/projects/aiimage0.png' | relative_url }})
![AI Image Analysis 2]({{ '/assets/img/projects/aiimage2.png' | relative_url }})
![AI Image Analysis 3]({{ '/assets/img/projects/aiimage3.png' | relative_url }})

## Key insight
For attention-heavy transformer workloads, runtime performance is frequently limited by **memory bandwidth and allocation behavior**, not pure compute. The most reliable gains came from aligning the execution path with hardware constraints (precision, transfers, allocation), rather than repeating training-only tuning.
