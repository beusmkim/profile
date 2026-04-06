---
layout: default
title: Home
---

# Beumsu Kim
### AI Engineer — Physical System Modeling, Learning-Based Control & On-Device AI

I work at the intersection of physical system modeling and AI.

My background spans characterizing dynamic system behavior through experiment, calibrating models against empirical data, and training learning-based systems under real hardware constraints.

From high-strain-rate material characterization (SHPB, Abaqus FEM) to large-scale VLM fine-tuning (LoRA, quantization) and on-device AI pipeline design — my work is grounded in measurement-driven validation at every stage.

---

## Core Competencies

- Physical system characterization & constitutive model calibration (SHPB, FEM)
- Experimental methodology: measure → model → calibrate → validate
- Large-scale VLM fine-tuning under GPU constraints (LoRA, INT8 quantization, ensemble)
- On-device AI system design (quantized ASR, slot-based LLM agent)
- Hardware-constrained inference optimization (FP16 / INT8, CUDA-aware execution)

---

## Representative Work

### SHPB Calibration — High-Strain-Rate Material Characterization & Model Validation  
Characterized dynamic material behavior via Split Hopkinson Pressure Bar experiments and calibrated a constitutive model against measured stress–strain curves.  
Validated parameters through Abaqus FEM simulation — applying the same measure → model → calibrate → validate workflow central to physical system identification in control engineering.

[**View project →**]({{ "/projects/11-shpb" | relative_url }})

---

### DailyLog — On-Device Voice AI Pipeline & Adaptive Recommendation System
🏆 Excellence Award — SSAFY Special Project (2026)
Built end-to-end voice journaling system: int8-quantized on-device ASR (~300ms), slot-based LLM agent for diary auto-generation, and Thompson Sampling recommendation engine.
Reduced diary completion time from ~20 min to ~5 min (~70%).

[**View project →**]({{ "/projects/12-dailylog" | relative_url }})

---

### VQA Fine-Tuning — Qwen3-VL LoRA Training & Ensemble  
Fine-tuned Qwen3-VL-8B-Instruct with LoRA on a VQA competition dataset, improving from a baseline of 0.76 to 0.96 Public Score.  
Explored model replacement, BLIP-based caption augmentation, hyperparameter search across 3 LoRA configurations, and logistic regression ensemble — achieving a final score of **0.96759**.

[**View project →**]({{ "/projects/09-vqa-qwen" | relative_url }})

---

## Engineering Philosophy

Performance ceilings are determined by constraint awareness.

I prioritize:
- Measurement before optimization
- Architectural isolation before micro-optimization
- Hardware-aligned execution over brute-force scaling
