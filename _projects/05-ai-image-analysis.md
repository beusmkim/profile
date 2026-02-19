
---
layout: project
title: "AI Image Analysis – GPU-Constrained Optimization"
image: /assets/img/projects/image-analysis-placeholder.jpg
---

## Overview
Image analysis pipeline optimized for low-end GPU environments with strict VRAM constraints.

## Technical Optimization

### Memory Efficiency
- FP32 → FP16 precision conversion
- Peak VRAM reduced by ≈35–40%
- Controlled tensor allocation to reduce fragmentation

### CUDA Execution Control
- Implemented asynchronous CUDA stream logic
- Reduced redundant tensor copies
- Improved throughput stability under concurrent requests

### Quantization Exploration
- Evaluated FP16 vs INT8 trade-offs
- Reduced inference time by ≈22% while maintaining acceptable accuracy

---
Focused on aligning model execution patterns with GPU memory hierarchy and compute utilization behavior.
