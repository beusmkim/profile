---
layout: project
title: "AI Image Analysis – Hardware-Constrained Inference Optimization"
image: /assets/img/projects/aiimage0.png
---

## Overview
This project focuses on optimizing transformer-based image analysis under constrained GPU environments.

## Technical Challenge
Frequent VRAM spikes and unstable inference latency due to memory saturation in attention layers.

## Optimization Strategy

### 1. Mixed Precision Deployment
- Converted FP32 to FP16
- Achieved ~38–40% peak VRAM reduction
- Reduced memory bandwidth pressure

### 2. Quantization Exploration
- Compared FP16 vs INT8 trade-offs
- Reduced end-to-end inference latency by ~22%
- Maintained acceptable accuracy

### 3. CUDA-Level Improvements
- Implemented asynchronous CUDA streams
- Reduced unnecessary GPU↔CPU tensor transfers
- Minimized memory fragmentation

## Key Insight
Performance bottlenecks were primarily memory-bandwidth bound rather than compute-bound, particularly in attention mechanisms.

This project demonstrates model-level performance reasoning aligned with AI silicon validation workflows.

## Screenshots
![AI Image 0]({{ '/assets/img/projects/aiimage0.png' | relative_url }})
![AI Image 2]({{ '/assets/img/projects/aiimage2.png' | relative_url }})
![AI Image 3]({{ '/assets/img/projects/aiimage3.png' | relative_url }})
