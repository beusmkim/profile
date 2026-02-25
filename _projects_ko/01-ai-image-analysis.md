---
layout: project
title: "AI Image Analysis — Memory-Bound 추론 최적화"
image: /assets/img/projects/aiimage0.png
category: hardware
priority: 1
---

## Overview

본 프로젝트는 transformer 기반 이미지 분석 모델의 추론 불안정성을 진단하고, GPU 메모리 제약 환경에서 런타임 병목을 완화하는 것을 목표로 했다.  
모델 용량을 키우는 대신 실행 경로를 최적화하는 접근을 택했다.

---

## Problem

데이터 증강과 하이퍼파라미터 튜닝으로 정확도는 개선되었으나 배포 환경에서는:

- Peak VRAM 스파이크로 간헐적 OOM 발생  
- 동시 추론 시 latency 분산 증가  
- 추가 학습은 런타임 개선으로 이어지지 않음  

문제는 모델 품질이 아니라 실행 효율이었다.

---

## Measurement Context

환경:
- GPU: NVIDIA A100 (Google Cloud)
- Batch size: 1–5 범위 동적 조정
- 동시 추론 환경

측정 도구:
- torch.profiler (kernel timing 및 memory trace)
- nvidia-smi VRAM 모니터링
- Roofline 모델 기반 memory vs compute 해석

---

## Diagnosis

관찰 결과:

- SM utilization이 compute peak에 도달하지 않음
- Attention-heavy layer에서 DRAM bandwidth 급증
- Q/K/V 텐서 이동이 global memory 트래픽 지배
- 중간 텐서 할당과 VRAM 스파이크가 일치

Arithmetic intensity가 낮고 메모리 트래픽이 높은 패턴으로, 해당 워크로드는 compute-bound가 아닌 memory-bandwidth bound 특성을 보였다.

---

## Approach

### Mixed Precision 적용 (FP16)
- FP32 → FP16 변환
- activation footprint 감소
- DRAM 압력 완화

### Quantization 탐색 (INT8)
- FP16 대비 INT8 벤치마크
- latency 개선 vs 출력 안정성 비교
- 배포 가능한 precision 선택

### CUDA 인지형 실행 개선
- CUDA streams 기반 비동기 실행
- CPU↔GPU 전송 감소
- 텐서 재사용 구조 개선
- 동시 요청 blocking 감소

---

## Result

- Peak VRAM ~38–40% 감소
- End-to-end latency ~22% 개선
- 동시 추론 환경에서 latency variance 감소
- A100 환경에서 OOM 제거

---

## Limitations

- 단일 A100 환경에서 검증
- INT8 적용 시 calibration 필요
- 추가 개선은 kernel-level 최적화 필요

---

## Key Insight

Transformer 기반 attention-heavy 추론은 compute보다 메모리 대역폭과 할당 동작에 의해 제한되는 경우가 많다.  
지속 가능한 성능 개선은 실행 경로를 하드웨어 제약에 맞추는 데서 나온다.
