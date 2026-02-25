---
layout: project
title: "OneTakeStudio - 연산 격리형 AI 추론 시스템"
image: /assets/img/projects/onetakestudio_mainpage.png
---

## Overview
실시간 스트리밍 경로와 GPU 추론 워크로드를 분리해 지연 안정성을 확보한 compute-isolated 추론 시스템입니다. 핵심은 모델 자체보다 시스템 아키텍처(격리, 오케스트레이션)를 통해 inference가 실시간 서비스 품질을 훼손하지 않게 만드는 것입니다.

## Problem
추론과 스트리밍이 하나의 경로에 결합되어 있을 때:
- 동시 요청에서 GPU contention과 blocking이 증가
- 무거운 추론 구간에서 스트리밍 품질이 저하
- 추론 확장(스케일링)이 곧 서비스 불안정으로 이어질 위험

## Diagnosis
단일 모델 병목보다 **자원 경합(resource contention)** 이 본질적인 문제였습니다.
- 추론이 CPU/GPU 시간을 스트리밍 경로와 경쟁
- 한 단계의 stall이 backpressure로 이어져 blocking이 전파
- 격리가 없으면 튜닝/스케일링이 항상 리스크를 동반

## Approach
### Compute isolation (MSA)
- 스트리밍(WebRTC) 레이어와 inference worker를 분리
- worker 오케스트레이션을 통해 경합을 제어

### Hardware-aware inference path
- inference worker에 FP16 적용으로 VRAM 압력 완화
- GPU 집약 작업이 I/O/스트리밍을 block하지 않도록 설계

### Scalability
- inference worker를 독립적으로 수평 확장 가능
- 격리를 먼저 확보한 뒤 최적화를 진행(안정성 우선)

## Result
- 동시 요청에서 blocking **~35% 감소**
- 스트리밍 경로의 지연 안정성이 개선
- worker 단위로 profiling/최적화를 진행할 수 있는 구조 확보

## Key insight
실시간 시스템에서는 아키텍처가 1차 성능 레버입니다. compute isolation을 통해 안정적인 baseline을 만들면, precision/커널 최적화 같은 모델 수준 개선이 서비스 품질을 해치지 않고 누적될 수 있습니다.
