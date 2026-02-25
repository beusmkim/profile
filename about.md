---
layout: default
title: About
---

# About

I am an AI Systems Engineer focused on hardware-aware model execution and runtime optimization. My work prioritizes measurable performance improvements under hardware constraints, especially where transformer workloads become memory-bandwidth limited.

## Technical profile
I work at the boundary between models and execution:

- Diagnose performance ceilings (memory-bound vs compute-bound behavior)
- Reduce VRAM footprint and bandwidth pressure (precision strategies, allocation patterns)
- Improve latency stability under concurrency (asynchronous execution, isolation)
- Design inference systems that scale without contention (workers, orchestration, distributed pipelines)

## Technical stack

### AI model execution
- PyTorch inference pipelines
- Transformer workload analysis (attention memory footprint)
- Mixed precision deployment (FP16)
- Quantization experiments (INT8) and accuracy/performance trade-offs

### GPU / runtime optimization
- CUDA-aware execution (streams / asynchronous execution concepts)
- VRAM footprint control and fragmentation mitigation
- Minimizing CPU↔GPU transfers and redundant tensor copies
- Interpreting latency and throughput under realistic concurrency

### Systems and scalability
- Microservice-based compute isolation (MSA) to prevent resource contention
- Worker-based orchestration for throughput stability
- AWS Batch + S3 distributed processing for large datasets
- Tile-based partitioning for memory-safe geospatial workloads

### Inference strategy engineering
- Multi-pass inference orchestration
- Consistency-based scoring and correction logic
- Post-processing as a system-level lever when training improvements plateau

## Evidence
- Peak VRAM reduction: ~38–40% via FP16 deployment
- Inference latency improvement: ~22% via precision/quantization strategy exploration
- Blocking reduction under concurrency: ~35% via compute isolation architecture

## Direction
My direction is to contribute to teams that care about model-level validation, runtime efficiency, and silicon-aligned performance reasoning—where real gains come from understanding execution, not just training.
