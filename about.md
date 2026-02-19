---
layout: default
title: About
---

# About

I build hardware-aware AI software focused on execution efficiency under real GPU constraints.
My scope is model runtime optimization, not RTL design.
I work on how kernels, precision strategy, memory behavior, and system architecture interact to determine delivered performance.

## Positioning Summary (Tesla AI Silicon)

- I optimize AI model execution where runtime behavior is constrained by VRAM, bandwidth, and scheduling.
- I treat performance as a systems problem: precision, memory traffic, stream concurrency, and contention control.
- I focus on measurable outcomes from production-style workloads, not synthetic benchmark tuning.
- I align software optimization work with silicon validation needs by exposing memory-bound bottlenecks and runtime limits.
- I can contribute across single-GPU optimization and distributed preprocessing pipelines used for large-scale evaluation.

## Technical Stack (Capability-Based)

### 1) Runtime Execution Optimization (CUDA-Oriented)
- CUDA-based inference optimization with asynchronous stream logic
- GPU runtime scheduling decisions based on observed blocking and contention patterns
- Kernel-level execution flow tuning to reduce avoidable stalls and transfer overhead

### 2) Precision and Latency/Memory Trade-off Engineering
- FP16 mixed-precision execution to reduce VRAM pressure while maintaining usable model quality
- INT8 quantization experiments to evaluate latency gains against precision-side risk
- Numeric format selection driven by runtime and memory behavior, not framework defaults

### 3) Memory-System Reasoning and Workload Characterization
- Memory-bound vs compute-bound workload diagnosis
- Transformer attention memory-footprint analysis for practical execution constraints
- VRAM footprint reduction and memory traffic-aware optimization decisions

### 4) Throughput Stability and Contention Isolation
- Microservice-based compute isolation (MSA) to separate inference and non-inference workloads
- Worker separation strategies to control GPU contention under concurrent request patterns
- Architecture choices driven by sustained throughput stability, not peak single-request numbers

### 5) Distributed Data/Validation Pipeline Execution
- AWS Batch + S3 based distributed processing pipelines for large-scale preprocessing jobs
- Partitioned batch execution design for scale-out and reproducible data preparation
- Infrastructure setup focused on reliable execution throughput across growing dataset volume

## Measured Impact

- FP16 mixed precision: approximately 38-40% peak VRAM reduction
- INT8 experiments: approximately 22% inference latency improvement
- Compute isolation and worker separation: approximately 35% blocking reduction in concurrent workloads
