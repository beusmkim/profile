---
layout: default
title: About
---

# About

I am an AI Systems Engineer focused on **hardware-aware model execution and runtime optimization**.

Unlike application-layer AI development, my work concentrates on how models interact with hardware constraints such as:

- GPU memory hierarchy
- Memory bandwidth saturation
- VRAM footprint management
- Compute-bound vs memory-bound behavior
- Precision trade-offs (FP16 / INT8)

---

## Technical Stack (Hardware-Aligned)

### AI Model Execution & Optimization
- PyTorch-based inference pipelines
- Mixed precision (FP16) deployment
- INT8 quantization experimentation
- Transformer attention memory footprint analysis
- End-to-end inference latency profiling

### GPU & CUDA Engineering
- CUDA stream-based asynchronous execution
- GPU memory allocation control
- Tensor transfer minimization (CPU↔GPU)
- Memory fragmentation mitigation
- VRAM utilization optimization (~38–40% reduction achieved)

### Performance & Runtime Reasoning
- Compute-bound vs memory-bound workload analysis
- Bottleneck identification in attention layers
- Precision vs performance trade-off evaluation
- Throughput stability under concurrent load (~22–27% latency improvement)

### Distributed & Scalable Systems
- Microservice-based compute isolation (MSA)
- GPU contention control via worker separation (~35% blocking reduction)
- AWS Batch + S3 distributed processing
- Tile-based partitioning for large-scale ERA5 datasets

---

## Engineering Direction

My goal is to operate at the intersection of:

- Model-level validation
- Runtime optimization
- Hardware-aligned inference execution
- AI silicon performance reasoning

I focus on maximizing effective hardware utilization rather than solely improving model accuracy.
