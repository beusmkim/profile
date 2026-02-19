---
layout: default
title: About
---

# About

I’m Beomsoo Kim, focusing on **hardware-aware AI software**—because real performance is decided by **memory, bandwidth, and execution behavior**, not just model accuracy.

## What I do
I work between **AI models** and **hardware execution**:

- CUDA-aware inference design (streams / async execution concepts)  
- Mixed precision (FP16) + quantization (INT8) trade-offs  
- Memory hierarchy awareness (VRAM footprint, allocation patterns, bandwidth bottlenecks)  
- System design for stable throughput (compute isolation, worker-based scaling)  

## Why this matters for AI silicon
AI chips succeed only when the software stack can:
- keep the accelerator **fed** (avoid memory stalls)  
- map model execution efficiently (avoid unnecessary transfers / redundant graphs)  
- validate performance using **real model behavior** (not synthetic benchmarks)  

## Evidence (quantified)
- **~38–40%** peak VRAM reduction via FP16 optimization  
- **~22–27%** inference latency improvement  
- **~35%** reduction in blocking under concurrent requests  

## What I’m aiming for
Model-level validation + runtime optimization aligned with silicon characteristics.
