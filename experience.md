---
layout: default
title: Experience
subtitle: "Execution history — roles, responsibilities, and measurable outcomes"
permalink: /experience
---

## Summary
My experience combines customer operations, applied AI projects, and system-level performance reasoning. I prioritize clear problem framing, measurable outcomes, and architecture-first improvements under real constraints (latency, memory, concurrency).

## Timeline (chronological)

### Samsung Software AI Academy For Youth (SSAFY)
**Role:** Project-based engineer (AI systems / applied ML)  
**Focus:** End-to-end AI prototyping, inference optimization, distributed pipelines, and system architecture

- **Problem:** Training improvements often plateau while deployment performance and reliability remain unstable (VRAM spikes, latency variance, contention under concurrency).
- **Approach:** Shifted optimization to the inference/runtime layer and system design.
  - Built hardware-aware inference optimizations (FP16 deployment, INT8 exploration, CUDA-aware execution concepts)
  - Designed compute isolation architectures (MSA) separating latency-sensitive paths from inference workers
  - Implemented scalable data pipelines for large datasets (tile-based partitioning, AWS Batch + S3 orchestration)
  - When training gains stalled (VQA), used inference orchestration (multi-pass inference + consistency scoring) to improve reliability without increasing model size
- **Result:** Delivered measurable improvements across projects:
  - Peak VRAM reduced by ~38–40% via FP16 deployment
  - Inference latency improved by ~22% via precision/quantization strategy exploration
  - Blocking reduced by ~35% under concurrency through compute isolation
  - Accuracy improved from 92% → 96.7% through inference-stage strategy design
- **Learning:** System performance is dictated by bandwidth, memory behavior, and contention as much as model quality. Architecture and runtime design create stable baselines where optimizations compound safely.

### LG U+ Retail / Sales Operations
**Role:** Sales Associate / Customer Operations  
**Focus:** Customer consultation, CRM execution, store performance improvement

- **Problem:** Improve conversion and customer flow with limited floor space and competing offers.
- **Approach:** Repositioned accessory placement and optimized store layout to align with customer movement patterns.
- **Result:** Improved cross-sell attachment and reduced consultation friction (tracked via daily sales mix and store KPIs).
- **Learning:** Operational constraints behave like system constraints; isolating bottlenecks and redesigning flow produces outsized gains.
