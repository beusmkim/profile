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
---

## Overview
Qwen 2.5-7B 기반 VQA 파이프라인에서 학습 개선이 정체된 이후, inference 단계의 오케스트레이션 전략으로 정확도를 개선한 사례입니다. 본 포트폴리오에서는 하드웨어 최적화 프로젝트 대비 우선순위를 낮게 두고, inference 전략 설계 역량을 보여주는 용도로 포함했습니다.

## Problem
데이터 증강과 하이퍼파라미터 튜닝으로 정확도 92%까지 개선했지만 이후 정체되었습니다.
- 추가 튜닝의 효용이 급격히 감소
- 학습 비용만 증가하고 성능은 유의미하게 오르지 않음
- 남은 오류는 inference 단계에서의 보정이 필요

## Diagnosis
정체의 핵심은 모델 용량이 아니라 **예측의 일관성 부족**이었습니다.
- 동일 입력에서도 후보 답안이 여러 개 생성
- 애매한 케이스에서 단일 패스 예측이 취약
- 시스템 레벨의 보정 로직이 필요

## Approach
### Multi-pass inference
- 동일 이미지/질문 쌍에 대해 반복 추론 수행
- 여러 후보 답안을 수집

### Consistency scoring + correction
- 룰 기반 점수 시스템으로 후보를 랭킹
- 합의도가 높은 답안을 강화하고 불안정한 출력을 보정

## Result
정확도 **92% → 96.7%**로 개선(모델 크기 증가 없이)

## Key insight
학습 개선이 정체될 때 inference 전략은 강력한 레버가 될 수 있습니다. multi-pass 추론과 일관성 기반 스코어링은 확률적 변동성을 신호로 바꿔 신뢰도를 높입니다.
