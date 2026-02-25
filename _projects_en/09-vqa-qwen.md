---
layout: project
title: "VQA System — Inference-Orchestrated Variance Reduction"
image: /assets/img/projects/vqa-qwen.jpg
category: ml
priority: 2
---

## Overview

A Visual Question Answering system built on Qwen 2.5-7B, redesigned to improve reliability when training improvements plateaued.

Instead of increasing model size or retraining complexity, the focus shifted to inference-stage variance control.

---

## Problem

After data augmentation and hyperparameter tuning, validation accuracy plateaued at 92%.

Observed issues:

- High variability in predictions for ambiguous inputs
- Stochastic instability across repeated inference calls
- Training iterations increased compute cost without significant gains

The bottleneck was not model capacity, but prediction consistency.

---

## Measurement Context

- Single-GPU inference evaluation
- Multiple repeated inference runs per input
- Accuracy measured across ambiguous validation samples

Observed:
- Output instability across identical inputs
- Confidence variance between candidate answers
- Performance degradation in edge-case reasoning

---

## Diagnosis

The model exhibited stochastic variance in uncertain regions.

This suggested that:

- Single-pass inference was brittle
- Variance reduction could improve reliability
- Inference orchestration could outperform additional training

---

## Approach

### Multi-Pass Inference

- Executed repeated inference per image-question pair
- Collected multiple candidate outputs

### Consistency-Based Scoring

- Ranked candidates based on agreement and confidence stability
- Penalized outlier predictions
- Reinforced consensus-driven outputs

### Structured Post-Processing

- Introduced deterministic correction logic
- Reduced output variance across runs

---

## Result

- Accuracy improved from 92% → 96.7%
- Reduced prediction instability in ambiguous cases
- Improved reliability without increasing model size

---

## Limitations

- Increased inference time due to repeated passes
- Not suitable for strict real-time systems
- Further improvements may require ensemble or calibration tuning

---

## Key Insight

When training improvements plateau, inference variance becomes a dominant factor.

Treating inference as a stochastic process and reducing output variance through orchestration can significantly improve system-level reliability without modifying model weights.

---

## Screenshots

![VQA Main]({{ '/assets/img/projects/vqa0.png' | relative_url }})
[Open vqa2 original]({{ '/assets/img/projects/vqa2.png' | relative_url }})
<a href="{{ '/assets/img/projects/vqa2.png' | relative_url }}" target="_blank" rel="noopener">
  <img class="long-vertical" src="{{ '/assets/img/projects/vqa2.png' | relative_url }}" alt="VQA Long Screenshot (vqa2)" />
</a>
