---
layout: default
title: Home
---

# Beumsu Kim
### AI Systems Engineer — Hardware-Constrained Inference & Runtime Optimization

I design AI systems by diagnosing execution bottlenecks under real hardware constraints.  
My work focuses on identifying whether performance ceilings are compute-bound or memory-bandwidth bound, and restructuring inference paths accordingly.

Rather than increasing model size, I optimize precision, tensor lifecycle, and system architecture to produce measurable runtime gains.

---

## Core Competencies

- Memory-bandwidth bound transformer diagnosis (attention-heavy workloads)
- Mixed precision and quantization trade-off analysis (FP16 / INT8)
- CUDA-aware execution reasoning and concurrency stabilization
- Compute isolation architecture for latency-sensitive systems
- Partitioned large-scale compute design (bounded memory execution)

---

## Representative Work

### AI Image Analysis — Memory-Bound Inference Optimization  
Diagnosed attention-heavy inference on NVIDIA A100 as bandwidth-bound via profiling and roofline reasoning.  
Reduced peak VRAM by ~38–40% and improved end-to-end latency by ~22% without increasing model capacity.  
[**View project →**]({{ "/projects/01-ai-image-analysis" | relative_url }})

---

### SHPB Calibration — Experimental Calibration & Model Validation  
Characterized high-strain-rate material behavior through Split Hopkinson Pressure Bar experiments.  
Calibrated constitutive parameters against measured stress-strain curves and improved simulation fidelity under dynamic loading.  
[**View project →**]({{ "/projects/11-shpb" | relative_url }})

---

### DailyLog — On-Device Voice AI Pipeline & Adaptive Recommendation System
🏆 Excellence Award — SSAFY Special Project (2026)
Built end-to-end voice journaling system: int8-quantized on-device ASR (~300ms), slot-based LLM agent for diary auto-generation, and Thompson Sampling recommendation engine.
Reduced diary completion time from ~20 min to ~5 min (~70%).

[**View project →**]({{ "/projects/12-dailylog" | relative_url }})

---

### OneTakeStudio — Compute-Isolated AI Inference System  
Redesigned architecture to decouple latency-sensitive streaming from GPU-bound inference workers.  
Reduced blocking under concurrency by ~35% and stabilized latency variance.  
[**View project →**]({{ "/projects/02-onetakestudio" | relative_url }})

---

### Satellite Data Center Siting — Partitioned Large-Scale Compute  
Built tile-based distributed pipeline for ERA5 datasets using AWS Batch + S3.  
Bounded per-task memory and improved iteration speed through modular recomputation design.  
[**View project →**]({{ "/projects/03-aws-dc-siting" | relative_url }})

---

## Engineering Philosophy

Performance ceilings are determined by constraint awareness.

I prioritize:
- Measurement before optimization
- Architectural isolation before micro-optimization
- Hardware-aligned execution over brute-force scaling
