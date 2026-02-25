---
layout: project
title: "VQA 시스템 — 추론 오케스트레이션 기반 분산 감소"
image: /assets/img/projects/vqa0.png
category: ml
priority: 2
---

## Overview

Qwen 2.5-7B 기반 VQA 시스템에서 학습 개선이 정체된 이후, 추론 단계의 분산(variance)을 줄이는 방식으로 성능을 개선한 프로젝트입니다.

모델을 키우는 대신, 추론 신뢰도를 구조적으로 향상시키는 접근을 선택했습니다.

---

## Problem

데이터 증강과 하이퍼파라미터 튜닝으로 정확도는 92%까지 개선되었으나 이후 정체되었습니다.

관찰된 문제:

- 동일 입력에서도 예측 결과가 흔들림
- 불확실 구간에서 예측 일관성 부족
- 추가 학습은 계산 비용만 증가

문제의 본질은 모델 용량이 아니라 추론 안정성이었습니다.

---

## Measurement Context

- 단일 GPU 환경에서 반복 추론 수행
- 동일 입력에 대해 여러 번 예측
- 모호한 검증 샘플 중심 평가

관찰:
- 동일 입력에서 출력 분산 존재
- 후보 답안 간 confidence 변동성
- edge case에서 불안정성 증가

---

## Diagnosis

모델은 불확실 구간에서 확률적 변동성을 보였습니다.

이는:

- 단일 추론이 취약함을 의미
- 분산 감소 전략이 필요함을 시사

---

## Approach

### Multi-Pass Inference

- 동일 이미지/질문에 대해 반복 추론
- 후보 답안 집합 생성

### Consistency Scoring

- 합의도와 confidence 기반 랭킹
- outlier 예측 패널티
- 일관성 높은 출력 강화

### 구조적 후처리

- deterministic correction 로직 도입
- 반복 실행 간 분산 감소

---

## Result

- 정확도 92% → 96.7% 개선
- 불확실 구간에서 신뢰도 향상
- 모델 구조 변경 없이 성능 개선

---

## Limitations

- 반복 추론으로 latency 증가
- 실시간 시스템에는 부적합
- 추가 개선은 calibration/ensemble 필요

---

## Key Insight

학습 개선이 정체될 경우, 추론 분산이 성능을 제한하는 주요 요소가 된다.

추론을 확률적 프로세스로 보고 분산을 제어하면, 가중치 변경 없이도 시스템 신뢰도를 향상시킬 수 있다.

---

## Screenshots

![VQA Main]({{ '/assets/img/projects/vqa0.png' | relative_url }})
[vqa2 원본 보기]({{ '/assets/img/projects/vqa2.png' | relative_url }})
<a href="{{ '/assets/img/projects/vqa2.png' | relative_url }}" target="_blank" rel="noopener">
  <img class="long-vertical" src="{{ '/assets/img/projects/vqa2.png' | relative_url }}" alt="VQA Long Screenshot (vqa2)" />
</a>
