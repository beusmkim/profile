---
layout: project
title: "AI Image Analysis — Memory-Bound Inference Optimization"
image: /assets/img/projects/aiimage0.png
---

## Overview

This project investigates inference instability in transformer-based image analysis under constrained GPU environments.  
The goal was not to increase model capacity, but to diagnose and mitigate runtime bottlenecks affecting VRAM usage and latency stability.

---

## Problem

After accuracy improvements through data augmentation and hyperparameter tuning, deployment performance remained unstable:

- Peak VRAM spikes triggered intermittent OOM failures  
- Latency variance increased under concurrent inference  
- Further training iterations did not improve runtime behavior  

The bottleneck was execution-level, not model-level.

---

## Measurement Context

Environment:
- GPU: NVIDIA A100 (Google Cloud)
- Batch size: 1–5 (dynamic adjustment)
- Concurrent inference calls

Profiling tools:
- torch.profiler (kernel-level timing and memory trace)
- nvidia-smi for runtime VRAM tracking
- Roofline reasoning for memory vs compute characterization

---

## Diagnosis

Profiling revealed:

- SM utilization remained below theoretical compute peak
- DRAM bandwidth usage spiked during attention-heavy layers
- Q/K/V tensor movement dominated memory traffic
- Intermediate tensor allocation aligned with VRAM spikes

Roofline interpretation indicated low arithmetic intensity relative to memory traffic, confirming the workload was memory-bandwidth bound rather than compute-bound.

---

## Hypothesis

If bandwidth and allocation behavior dominate:

- Reducing tensor footprint should reduce DRAM pressure
- Lower precision may improve bandwidth efficiency
- Tensor lifecycle control may stabilize VRAM spikes

---

## Approach

### Mixed Precision Deployment (FP16)
- Converted FP32 inference path to FP16 in numerically stable regions
- Reduced activation footprint and memory traffic

### Quantization Exploration (INT8)
- Benchmarked FP16 vs INT8
- Evaluated latency gain vs output stability
- Selected deployment-safe precision configuration

### CUDA-Aware Execution Improvements
- Applied asynchronous execution concepts (CUDA streams)
- Reduced redundant CPU↔GPU transfers
- Improved tensor reuse to mitigate fragmentation
- Structured execution path to reduce blocking under concurrency

---

## Result

- Peak VRAM reduced by ~38–40%
- End-to-end inference latency improved by ~22%
- Latency variance reduced under concurrency
- OOM failures eliminated under tested A100 setup

---

## Limitations

- Validated on single A100 environment
- INT8 required calibration for stability
- Further gains may require kernel-level fusion or C++ optimization

---

## Key Insight

Attention-heavy transformer inference is often constrained by memory bandwidth and allocation behavior rather than raw compute throughput.  
Sustainable performance gains emerged from aligning precision, tensor lifecycle, and execution patterns with hardware limitations.