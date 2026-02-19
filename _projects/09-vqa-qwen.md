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
데이터 증강/하이퍼파라미터 조정으로 92%까지 성능을 끌어올렸지만, 이후 개선이 정체되었습니다.  
단순 튜닝 반복이 아닌, **추론 단계의 전략**이 필요했습니다.

## Approach
- 이미지 증강과 하이퍼파라미터 조정으로 Qwen 2.5-7B 기반 모델 학습
- 성능 정체 이후, 룰 기반 점수 시스템을 도입  
  - 동일 이미지에 대해 여러 번 예측을 수행  
  - 예측된 후보들에 점수를 부여하고 최종 답안을 보정(일관성 강화)

## Result
- 정확도 92% → **96.7%**로 개선
- “학습만으로 안 되는 구간”에서 추론/보정 전략으로 성능을 끌어올리는 접근을 체득

## Learnings
- 모델링 외에도 전처리/후처리·추론 전략이 제품 성능을 결정하는 핵심 축이 될 수 있음
