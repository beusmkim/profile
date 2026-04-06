---
layout: project
title: "VLM 파인튜닝 — Qwen3-VL LoRA 학습 & 앙상블"
image: /assets/img/projects/vqa0.png
category: hardware
priority: 2
---

## Overview

VQA 대회 데이터셋에서 대형 비전-언어 모델(Qwen3-VL-8B-Instruct)을 LoRA로 파인튜닝하여, Baseline 0.76에서 최종 Public Score **0.96759**까지 개선한 프로젝트입니다.

모델 선택, 보조 모델 실험, 3가지 LoRA 설정 하이퍼파라미터 탐색, 로지스틱 회귀 앙상블까지 — 모두 고정된 GPU 메모리 제약 내에서 수행했습니다.

비전-언어 모델(VLM)은 로봇 학습과 조작에 활용되는 VLA(Vision-Language-Action) 시스템의 핵심 아키텍처입니다. 이 프로젝트는 실제 하드웨어 제약 하에서 대형 멀티모달 모델을 효율적으로 학습하는 경험을 제공했습니다.

---

## Problem

제공된 Baseline 모델은 **Qwen2.5-VL-3B-Instruct**로, Public Score **0.76028** — 목표 성능 수준에 미치지 못했습니다.

과제는 단순한 모델 교체가 아니라, 주어진 GPU 메모리 예산 내에서 학습 가능한 모델들 중 최고 성능을 찾는 것이었습니다.

---

## Step 1 — 모델 교체

**Qwen2.5-VL-3B-Instruct → Qwen3-VL-8B-Instruct**

벤치마크 성능과 메모리 실현 가능성을 함께 고려해 후보 모델들을 평가했습니다.  
Qwen3-VL-8B-Instruct가 주어진 제약 내에서 학습 가능한 최고 성능 모델로 선택되었습니다.

| 모델 | Public Score |
|---|---|
| Qwen2.5-VL-3B-Instruct (Baseline) | 0.76028 |
| Qwen3-VL-8B-Instruct | 0.90174 |

---

## Step 2 — 보조 모델 실험 (BLIP 캡션)

BLIP 모델을 전처리 단계에 도입하여 각 이미지의 캡션을 생성하고, 생성된 캡션을 학습 레이블에 추가해 학습 신호를 풍부하게 만들었습니다.

| 설정 | Public Score |
|---|---|
| Qwen3-VL-8B (캡션 없음) | 0.90174 |
| Qwen3-VL-8B + BLIP 캡션 | 0.92849 |

성능 향상은 확인되었으나, BLIP의 메모리 점유율과 학습 시간 대비 기대 이하의 성능 향상으로 이후 실험에서 제외했습니다.

---

## Step 3 — LoRA 하이퍼파라미터 탐색

Rank, 학습률, 양자화, Target Module 구성을 달리한 LoRA 3가지 변형을 학습했습니다.  
일반화 성능 향상을 위해, 데이터 로드 시 **선지를 무작위로 셔플**하여 동일 데이터를 반복 학습할 때도 정답 위치가 계속 달라지도록 조정했습니다.

| | 모델 1 | 모델 2 | 모델 3 |
|---|---|---|---|
| LoRA Rank | 16 | 32 | 32 |
| Learning Rate | 1e-4 | 1.5e-4 | 1.5e-4 |
| Epochs | 3 | 3 | 3 |
| 양자화 | None (16bit) | None (16bit) | 8bit |
| Target Modules | q/k/v/o\_proj | q/k/v/o\_proj | q/k/v/o\_proj + gate/up/down\_proj |
| Public Score | **0.96193** | 0.95884 | **0.96244** |

---

## Step 4 — 로지스틱 회귀 앙상블

3개 모델 각각에서 모든 문제에 대해 선지별(a/b/c/d) 확률을 계산했습니다.  
이 확률 벡터들을 하나로 통합하여 **로지스틱 회귀 메타 모델**의 입력으로 사용, 각 모델의 예측을 최적으로 결합했습니다.

**최종 Public Score: 0.96759**

---

## Key Insight

GPU 제약 하에서 대형 VLM을 효율적으로 학습하려면, 모델 규모·보조 입력·LoRA 설정·앙상블 전략에 걸친 체계적인 실험이 필요합니다.

각 단계를 측정 가능하고 비교 가능하게 설계한 구조적 ablation은, 학습된 모델을 물리적 제어 시스템에 통합할 때 각 컴포넌트의 신뢰성을 검증하는 방식과 동일한 사고방식을 따릅니다.

---

## Screenshots

![System Instruction & 프롬프트 빌더]({{ '/assets/img/projects/VLA3.png' | relative_url }})

![추론 프롬프트 (셔플 없음)]({{ '/assets/img/projects/VLA1.png' | relative_url }})

![BLIP 캡션 프롬프트]({{ '/assets/img/projects/VLA2.png' | relative_url }})

![앙상블 — 메타모델 결과]({{ '/assets/img/projects/VLA4.png' | relative_url }})
