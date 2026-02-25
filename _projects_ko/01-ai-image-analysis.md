---
layout: project
title: "AI 이미지 분석 - 메모리 병목 추론 최적화"
image: /assets/img/projects/aiimage0.png
---

## Overview
제한된 GPU 자원 환경에서 transformer 기반 이미지 분석 추론의 안정성과 효율을 개선한 사례입니다. 모델 규모를 키우는 대신 VRAM 압력과 메모리 대역폭 병목을 줄여 실제 워크로드에서 추론이 안정적으로 동작하도록 만드는 것이 목표였습니다.

## Problem
학습 단계에서 데이터 증강/하이퍼파라미터 튜닝을 통해 품질을 끌어올렸지만, 배포 환경에서는 성능 문제가 남아있었습니다.
- Peak VRAM 스파이크로 OOM이 간헐적으로 발생
- 동시 요청에서 latency 분산(variance)이 증가
- 추가 학습으로는 runtime 병목이 해결되지 않음

## Diagnosis
증상과 관찰을 기반으로 attention-heavy 실행 구간에서 **memory-bandwidth bound** 특성이 강하다고 판단했습니다.
- Q/K/V 텐서 이동이 많아 global memory 압력이 증가
- compute utilization이 포화되기 전에 latency가 상승
- 메모리 할당 패턴이 fragmentation과 VRAM 스파이크를 유발

## Approach
### Mixed precision 적용 (FP16)
- FP32 추론 경로를 FP16으로 전환(안전한 구간 중심)
- activation/tensor footprint를 줄여 대역폭 압력 완화

### Quantization 탐색 (INT8)
- FP16 vs INT8 trade-off를 대표 입력 기준으로 비교
- latency 개선을 우선하면서 출력 품질 안정성 모니터링

### CUDA 인지형 runtime 개선
- CUDA streams 기반 비동기 실행 개념 적용
- 불필요한 CPU↔GPU 이동 및 중복 copy 감소
- allocation/reuse 패턴을 개선해 fragmentation 완화

## Result
- Peak VRAM **~38-40% 감소** (FP16 적용)
- 추론 latency **~22% 개선** (precision/quantization 전략 탐색)
- 제한된 GPU 환경에서 OOM 발생과 latency variance가 감소하며 안정성 향상

## Key insight
attention-heavy transformer 워크로드는 compute보다 **메모리 대역폭과 할당 동작**에 의해 성능이 제한되는 경우가 많았습니다. 반복적인 학습 튜닝보다 실행 경로를 하드웨어 제약(precision, transfers, allocation)에 맞추는 것이 더 일관된 성능 개선으로 이어졌습니다.
