---
layout: default
title: About
---

# About

I am an AI Systems Engineer specializing in hardware-constrained inference optimization.

My work focuses on diagnosing execution bottlenecks under real GPU environments and restructuring inference paths based on measurable constraints such as memory bandwidth, VRAM allocation behavior, and concurrency pressure.

Rather than scaling models, I prioritize execution-level reasoning.

---

## Core Capabilities

I operate at the boundary between model design and hardware execution:

- Identify performance ceilings (memory-bound vs compute-bound)
- Characterize transformer attention workloads under bandwidth pressure
- Optimize precision strategies (FP16, INT8) with deployment-aware trade-offs
- Stabilize latency under concurrent inference
- Architect compute isolation for real-time AI systems
- Design partitioned execution pipelines for large-scale workloads

---

## Technical Stack (Capability-Oriented)

### AI Execution & Profiling
- PyTorch inference pipelines
- torch.profiler for kernel-level timing
- Transformer attention memory footprint analysis
- Roofline reasoning (arithmetic intensity vs bandwidth behavior)

### Precision & Runtime Optimization
- Mixed precision deployment (FP16)
- Quantization experimentation (INT8)
- Tensor lifecycle optimization
- CPU↔GPU transfer minimization
- Concurrency-aware execution restructuring

### System Architecture
- Microservice-based compute isolation (MSA)
- Worker orchestration for resource arbitration
- Latency-sensitive path separation
- Scalable distributed execution (AWS Batch, S3)

---

## Representative Evidence

- Peak VRAM reduction: ~38–40% via FP16 deployment
- Inference latency improvement: ~22% through precision and execution restructuring
- Blocking reduction: ~35% via compute isolation architecture
- Accuracy improvement (92% → 96.7%) via inference-stage variance reduction

---

## Engineering Philosophy

Performance ceilings are defined by constraints, not ambition.

I prioritize:
- Measurement before optimization
- Architectural isolation before micro-tuning
- Hardware-aligned execution over brute-force scaling

My direction is to contribute to teams focused on AI silicon validation, runtime efficiency, and hardware-software integration.