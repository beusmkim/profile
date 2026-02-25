---
layout: default
title: About
permalink: /ko/about
---

# About

저는 하드웨어 제약 환경에서 AI 추론 성능을 최적화하는 AI 시스템 엔지니어입니다.

실제 GPU 환경에서 실행 병목을 진단하고, 메모리 대역폭·VRAM 할당 동작·동시성 압력과 같은 측정 가능한 제약을 기준으로 추론 경로를 재설계합니다.

모델을 키우는 대신, 실행 구조를 바꾸는 접근을 우선합니다.

---

## Core Capabilities

저는 모델 설계와 하드웨어 실행 사이 경계에서 다음을 수행합니다.

- memory-bound vs compute-bound 성능 상한 진단
- transformer attention 워크로드의 대역폭 특성 분석
- FP16 / INT8 기반 precision 전략 설계 및 trade-off 분석
- 동시 추론 환경에서 latency 안정화
- 실시간 시스템을 위한 compute isolation 아키텍처 설계
- 대규모 데이터 처리를 위한 분할 기반 실행 구조 설계

---

## Technical Stack (역량 중심 정리)

### AI 실행 및 프로파일링
- PyTorch 추론 파이프라인
- torch.profiler 기반 kernel-level 분석
- Transformer attention 메모리 풋프린트 분석
- Roofline 관점의 arithmetic intensity 해석

### Precision 및 런타임 최적화
- Mixed precision 배포 (FP16)
- Quantization 실험 (INT8)
- 텐서 생명주기 및 메모리 할당 최적화
- CPU↔GPU 전송 최소화
- 동시성 환경에 맞춘 실행 경로 재구성

### 시스템 아키텍처
- MSA 기반 compute isolation 설계
- 워커 오케스트레이션을 통한 자원 경합 제어
- latency-sensitive 경로 분리
- AWS Batch + S3 기반 분산 실행 구조

---

## 정량 근거

- FP16 적용으로 Peak VRAM ~38–40% 감소
- Precision 및 실행 구조 개선으로 Latency ~22% 개선
- Compute isolation으로 동시 요청 blocking ~35% 감소
- 추론 단계 전략으로 정확도 92% → 96.7% 개선

---

## Engineering Philosophy

성능의 상한은 목표가 아니라 제약 조건에 의해 결정됩니다.

저는 다음을 우선합니다:
- 최적화 전에 측정
- 미세 조정보다 아키텍처 격리
- 무작정 스케일링보다 하드웨어 정렬된 실행 설계

AI 실리콘 검증, 런타임 효율, HW-SW 통합을 다루는 팀에서 기여하는 것이 목표입니다.