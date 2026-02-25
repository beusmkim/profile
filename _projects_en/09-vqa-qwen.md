---
layout: project
title: "VQA System — Inference-Orchestrated Accuracy Optimization"
image: /assets/img/projects/vqa-qwen.jpg
---

## Overview
A visual question answering system built on a Qwen 2.5-7B based pipeline. This project is included as a lower-priority case study to demonstrate inference-stage strategy design when training improvements plateau.

## Problem
Data augmentation and hyperparameter tuning pushed accuracy to 92%, but improvements stalled:
- Additional tuning produced diminishing returns
- Training-only iterations increased cost without meaningful gains
- The remaining error modes required inference-stage handling

## Diagnosis
The plateau was driven by **prediction inconsistency** rather than model capacity:
- The same input produced multiple plausible candidates
- Errors clustered around ambiguous cases where a single pass was brittle
- Improving accuracy required system-level correction logic

## Approach
### Multi-pass inference
- Performed repeated predictions for the same image-question pair
- Collected candidate answers across multiple runs

### Consistency-based scoring and correction
- Introduced a rule-based scoring layer to rank candidates
- Reinforced outputs with higher agreement and stable confidence
- Applied correction logic to improve consistency

## Result
Accuracy improved from **92% → 96.7%** without increasing model size.

## Key insight
When training gains plateau, system-level inference strategy can be an effective lever. Multi-pass inference with consistency scoring improves reliability by turning stochastic variability into a signal.
