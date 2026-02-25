---
layout: default
title: Home
---

# Beumsu Kim
### Hardware-Aware AI Systems Engineer (CUDA · FP16/INT8 · Memory/Latency)

I focus on aligning AI model execution with hardware constraints—memory bandwidth, VRAM footprint, and runtime behavior—so systems remain stable and efficient under real workload pressure.

## What I optimize
- Memory-bound transformer execution (attention-heavy workloads)
- Precision and deployment trade-offs (FP16, INT8)
- GPU utilization and latency stability under concurrency
- Inference system architecture (compute isolation, distributed workers)

## Featured work (most relevant to AI silicon / runtime optimization)
- **AI Image Analysis — Memory-Bound Inference Optimization**  
  FP16 reduced peak VRAM by ~38–40%, INT8 exploration improved latency by ~22%, and CUDA-level changes improved stability under constrained GPUs.  
  [**View project →**]({{ "/projects/01-ai-image-analysis" | relative_url }})

- **OneTakeStudio — Compute-Isolated AI Inference System**  
  Separated streaming and inference workers to reduce contention and improved blocking behavior by ~35% under concurrent workloads.  
  [**View project →**]({{ "/projects/02-onetakestudio" | relative_url }})

- **Satellite Data Center Siting — Distributed Geospatial Compute**  
  Tile-based partitioning + AWS Batch/S3 pipeline for large ERA5 datasets, designed for memory-safe horizontal scaling.  
  [**View project →**]({{ "/projects/03-aws-dc-siting" | relative_url }})
