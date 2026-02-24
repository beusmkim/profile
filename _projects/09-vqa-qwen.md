---
layout: project
title: VQA(Visual Question Answering) — 성능 정체를 넘기기 위한 룰 기반 보정
summary: "Qwen 2.5-7B 학습 후 92% 정체 구간에서, 룰 기반 점수/다중 예측 보정으로 96.7%까지 개선"
title_en: "VQA Rule-based Calibration Beyond Performance Plateau"
summary_en: "After Qwen 2.5-7B plateaued around 92%, improved to 96.7% with rule-based scoring and multi-pass prediction calibration."
period: "2026"
role: "AI Engineer"
stack: "Data Augmentation, Fine-tuning, Inference Strategy"
image: /assets/img/projects/vqa-qwen.jpg
order: 45
featured: true
links:
  - label: "Repository"
    url: "https://github.com/BeusmKim/REPO"
---

## Problem
Model accuracy plateaued at 92% despite extensive data augmentation and hyperparameter tuning.

Further training iterations yielded diminishing returns, indicating that model capacity was not the primary bottleneck.

A different inference-level strategy was required.

## Approach
Instead of continuing model-level tuning, I redesigned the inference pipeline:

- Built a multi-pass inference strategy using a Qwen 2.5-7B based model
- Performed repeated predictions on the same input image
- Introduced a rule-based scoring system to evaluate prediction consistency
- Applied answer correction logic based on confidence and agreement

This shifted optimization from training-level improvements to inference-time reasoning.

## Result
Accuracy improved from 92% → 96.7%

The gain was achieved without increasing model size or retraining complexity,
but through inference-level orchestration.

## Key Insight
Performance bottlenecks are not always solved at the model training stage.

Inference-time strategy, consistency filtering, and structured post-processing
can significantly improve system-level accuracy without additional compute cost.

## Problem (KR)
데이터 증강 및 하이퍼파라미터 튜닝으로 92%까지 정확도를 올렸으나,
이후 성능 개선이 정체되었습니다.

추가 학습은 계산 비용만 증가시키고 실질적 성능 향상은 제한적이었습니다.

## Approach (KR)
학습 중심 접근을 중단하고, 추론 단계 구조를 재설계했습니다.

- Qwen 2.5-7B 기반 다중 추론 전략 설계
- 동일 이미지에 대해 반복 추론 수행
- 예측 결과 간 일관성 기반 점수 시스템 도입
- 신뢰도 기반 최종 답안 보정 로직 구현

이는 모델 자체를 바꾸는 것이 아니라,
추론 오케스트레이션 구조를 개선하는 접근이었습니다.

## Result (KR)
정확도 92% → 96.7%로 향상

추가 학습 비용 없이, 추론 전략 재설계만으로 성능을 개선했습니다.

## Learnings (KR)
모델 정확도는 학습 단계에서만 결정되지 않습니다.

추론 단계의 구조적 설계,
후처리 로직,
일관성 기반 필터링은

제품 수준의 성능을 좌우하는 핵심 요소입니다.

## Screenshots
![VQA Main]({{ '/assets/img/projects/vqa0.png' | relative_url }})
[vqa2 원본 보기]({{ '/assets/img/projects/vqa2.png' | relative_url }})
![VQA Long Screenshot (vqa2)]({{ '/assets/img/projects/vqa2.png' | relative_url }})
