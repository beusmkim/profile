---
layout: project
title: "VLM Fine-Tuning — Qwen3-VL LoRA Training & Ensemble for VQA"
image: /assets/img/projects/vqa0.png
category: hardware
priority: 2
---

## Overview

Fine-tuned a large Vision-Language Model (Qwen3-VL-8B-Instruct) on a VQA competition dataset using LoRA, advancing from a baseline score of 0.76 to a final Public Score of **0.96759**.

The project involved systematic model selection, auxiliary model experiments, hyperparameter search across multiple LoRA configurations, and a logistic regression ensemble — all within fixed GPU memory constraints.

Vision-Language Models are the architectural backbone of VLA (Vision-Language-Action) systems increasingly used in robot learning and manipulation. This project provided hands-on experience in efficiently training and scaling such models under real hardware limits.

---

## Problem

The provided baseline used **Qwen2.5-VL-3B-Instruct**, which scored **0.76028** — insufficient for the target performance level.

The challenge was not just model selection, but finding the highest-performing model that could still be trained within the available GPU memory budget.

---

## Step 1 — Model Replacement

**Qwen2.5-VL-3B-Instruct → Qwen3-VL-8B-Instruct**

Evaluated candidate models by balancing benchmark performance against memory feasibility.  
Qwen3-VL-8B-Instruct was selected as the highest-performing model trainable within the given constraints.

| Model | Public Score |
|---|---|
| Qwen2.5-VL-3B-Instruct (baseline) | 0.76028 |
| Qwen3-VL-8B-Instruct | 0.90174 |

---

## Step 2 — Auxiliary Model Experiment (BLIP Captioning)

Introduced BLIP as a preprocessing step to generate image captions, which were appended to training labels to enrich the learning signal.

| Configuration | Public Score |
|---|---|
| Qwen3-VL-8B (no captioning) | 0.90174 |
| Qwen3-VL-8B + BLIP Captioning | 0.92849 |

While the gain was measurable, BLIP's memory and compute overhead relative to its marginal improvement made it impractical for subsequent experiments. Dropped in later stages.

---

## Step 3 — LoRA Hyperparameter Search

Trained three LoRA variants with different rank, learning rate, quantization, and target module configurations.  
To improve generalization, answer choices were **randomly shuffled during data loading** so that the correct answer position varied across training passes on the same sample.

| | Model 1 | Model 2 | Model 3 |
|---|---|---|---|
| LoRA Rank | 16 | 32 | 32 |
| Learning Rate | 1e-4 | 1.5e-4 | 1.5e-4 |
| Epochs | 3 | 3 | 3 |
| Quantization | None (16bit) | None (16bit) | 8bit |
| Target Modules | q/k/v/o\_proj | q/k/v/o\_proj | q/k/v/o\_proj + gate/up/down\_proj |
| Public Score | **0.96193** | 0.95884 | **0.96244** |

---

## Step 4 — Logistic Regression Ensemble

Each of the three models was evaluated to produce per-choice probabilities (a/b/c/d) for every question.  
These probability vectors were concatenated and fed into a **logistic regression meta-model**, which learned how to optimally weight each model's predictions.

**Final Public Score: 0.96759**

---

## Key Insight

Training a large VLM efficiently under GPU constraints requires iterative experimentation across model scale, auxiliary inputs, LoRA configuration, and ensemble strategy.

The structured ablation — each step measurable and comparable — mirrors the kind of systematic validation required when integrating learned models into physical control systems, where confidence in each component matters.

---

## Screenshots

![System Instruction & Prompt Builder]({{ '/assets/img/projects/VLA3.png' | relative_url }})

![Inference Prompt (no shuffle)]({{ '/assets/img/projects/VLA1.png' | relative_url }})

![BLIP Caption Prompt]({{ '/assets/img/projects/VLA2.png' | relative_url }})

![Ensemble — Meta Model Results]({{ '/assets/img/projects/VLA4.png' | relative_url }})
