---
layout: default
title: Experience
subtitle: "Execution history — roles, responsibilities, and measurable outcomes"
permalink: /ko/experience
---

## Summary
저는 고객 운영 경험과 AI/시스템 프로젝트 경험을 결합해, 문제 정의와 지표 중심의 개선을 우선합니다. 특히 latency, memory, 동시성 제약이 있는 환경에서 아키텍처와 런타임 최적화를 통해 재현 가능한 성능 개선을 만드는 데 강점이 있습니다.

## Timeline

### Samsung Software AI Academy For Youth (SSAFY)
**역할:** 프로젝트 기반 엔지니어(AI 시스템 / Applied ML)  
**초점:** 엔드투엔드 프로토타이핑, 추론 최적화, 분산 파이프라인, 시스템 아키텍처

- **문제:** 학습 성능 개선이 정체되는 동안, 배포 환경 성능과 안정성(VRAM 스파이크, latency variance, 동시성 경합)이 병목이 되는 경우가 많았습니다.
- **접근:** 학습 중심에서 벗어나 추론/런타임 레이어와 시스템 설계로 최적화 레버를 이동했습니다.
  - 하드웨어 인지형 추론 최적화(FP16 적용, INT8 탐색, CUDA 인지형 실행 개념)
  - latency-sensitive 경로와 inference worker를 분리하는 compute isolation(MSA) 설계
  - 대용량 데이터 처리를 위한 분산 파이프라인(tile partitioning, AWS Batch + S3 오케스트레이션)
  - VQA에서는 학습 정체 이후 multi-pass inference + 일관성 스코어링으로 추론 단계에서 신뢰도를 강화
- **결과:** 프로젝트 전반에서 정량 성과를 확보했습니다.
  - FP16 적용으로 peak VRAM ~38–40% 감소
  - precision/quantization 탐색으로 latency ~22% 개선
  - compute isolation으로 동시 요청 blocking ~35% 감소
  - inference 전략으로 정확도 92% → 96.7% 개선
- **학습:** 실제 성능은 모델 품질뿐 아니라 대역폭, 메모리 동작, 경합에 의해 결정됩니다. 아키텍처로 안정적인 baseline을 만든 뒤 최적화를 누적하는 접근이 가장 재현 가능했습니다.

### LG U+ Retail / Sales Operations
- 고객 상담/운영 환경에서 병목을 정의하고, 동선과 의사결정 흐름을 개선하는 방식으로 성과를 만들었습니다.
