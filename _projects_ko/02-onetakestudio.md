---
layout: project
title: "OneTakeStudio — Compute-Isolated AI 추론 시스템"
image: /assets/img/projects/onetakestudio_mainpage.png
---

## Overview

실시간 스트리밍과 AI 추론을 분리해 지연 안정성을 확보한 시스템 설계 프로젝트.

---

## Problem

추론과 스트리밍이 동일 실행 경로에 있을 때:

- 동시 요청 시 GPU contention 발생
- 추론 지연이 스트리밍으로 전파
- backpressure가 연쇄적으로 발생

문제는 모델이 아니라 구조였다.

---

## Measurement Context

- 동시 추론 요청 환경
- GPU 사용률 모니터링
- 프레임 드롭 상관 분석

관찰:
- GPU 사용률 급증 시 스트리밍 FPS 저하
- inference burst와 blocking 이벤트가 일치

---

## Diagnosis

스트리밍 I/O와 추론 연산 간 자원 경합이 지연 불안정의 원인이었다.

---

## Approach

### Compute Isolation (MSA)
- 스트리밍과 추론 워커 완전 분리
- 워커 기반 오케스트레이션 도입

### 하드웨어 인지형 설계
- 추론 워커 내부 FP16 적용
- GPU 집약 작업이 I/O를 block하지 않도록 설계

### 확장성
- 워커 수평 확장
- 스케일링 중에도 스트리밍 지연 유지

---

## Result

- Blocking 약 35% 감소
- 지연 분산 안정화
- 추후 하드웨어 최적화를 위한 구조적 기반 확보

---

## Insight

실시간 AI 시스템에서는 모델보다 구조가 성능 상한을 결정한다.  
Critical path 격리는 하드웨어-소프트웨어 통합 설계와 유사한 원칙을 따른다.