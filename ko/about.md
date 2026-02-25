---
layout: default
title: About
permalink: /ko/about
---

# About

저는 하드웨어 제약 조건에서 AI 추론 성능을 개선하는 데 집중하는 AI 시스템 엔지니어입니다. transformer 워크로드가 메모리 대역폭에 의해 제한되는 구간에서, 실행 경로를 재설계해 VRAM 사용과 지연 안정성을 개선하는 작업을 수행해왔습니다.

## 기술 프로필
저는 모델과 실행 사이 경계에서 다음을 수행합니다.

- 성능 상한 진단(memory-bound vs compute-bound)
- VRAM 풋프린트/대역폭 압력 감소(precision 전략, allocation 패턴)
- 동시성에서 latency 안정화(비동기 실행 개념, 격리)
- 경합 없이 확장 가능한 추론 시스템 설계(워커, 오케스트레이션, 분산 파이프라인)

## 기술 스택

### AI 모델 실행
- PyTorch 기반 추론 파이프라인
- attention memory footprint 분석(Transformer workload)
- Mixed precision(FP16) 배포
- Quantization(INT8) 탐색 및 품질-성능 트레이드오프

### GPU / 런타임 최적화
- CUDA 인지형 실행(Streams/비동기 실행 개념)
- VRAM 풋프린트 제어 및 fragmentation 완화
- CPU↔GPU 이동/중복 텐서 복사 최소화
- 동시 요청 환경에서 지연/처리량 해석 및 안정화

### 시스템/스케일
- MSA 기반 compute isolation(자원 경합 방지)
- 워커 오케스트레이션으로 처리량 안정화
- AWS Batch + S3 분산 처리(대용량 데이터)
- Tile-based partitioning(메모리 상한을 고정하는 분할 전략)

### 추론 전략 엔지니어링
- multi-pass inference 오케스트레이션
- 일관성 기반 스코어링/보정 로직
- 학습 개선 정체 시 후처리/추론 전략을 시스템 레버로 활용

## 성과
- FP16 적용으로 peak VRAM ~38–40% 감소
- precision/quantization 탐색으로 latency ~22% 개선
- compute isolation으로 동시 요청 blocking ~35% 감소

## 지향점
학습 성능이 아니라 실행 효율과 재현 가능한 개선을 기준으로, 모델 수준 검증과 런타임 최적화, 그리고 실리콘 특성에 맞춘 성능 추론이 필요한 팀에서 기여하는 것을 목표로 합니다.
