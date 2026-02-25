---
layout: project
title: "Satellite Data Center Siting — 분할 기반 대규모 연산 설계"
image: /assets/img/projects/dc-siting-placeholder.jpg
category: hardware
priority: 4
---

## Overview

ERA5 위성 데이터를 활용해 데이터센터 입지를 평가하는 분산 지리 연산 파이프라인입니다.

핵심은 대용량 데이터 처리 시 메모리 상한을 제어하는 분할 기반 실행 설계입니다.

---

## Problem

ERA5(zarr) 데이터는 단일 메모리 로딩에 부적합한 대용량 구조입니다.

관찰된 문제:

- 광범위 집계 시 메모리 사용량 급증
- 단일 실행 구조에서 반복 실험 속도 저하
- 중간 데이터 생성 시 메모리 스파이크 발생

---

## Diagnosis

성능 병목은 연산량이 아니라 데이터 이동과 집계 구조였습니다.

분할 전략이 없으면 메모리 상한을 제어할 수 없습니다.

---

## Approach

### Tile-Based Partitioning

- 지리 데이터를 타일 단위로 분할
- 작업별 메모리 사용량을 제한
- 점진적 집계 가능 구조 설계

### 분산 실행

- AWS Batch 기반 병렬 처리
- S3 중간 산출물 저장
- 재실행 경계를 명확히 정의

### 추상화 계층

- node-level scoring abstraction 도입
- 향후 피처 확장 시 구조 변경 최소화

---

## Result

- 수평 확장 가능한 파이프라인 확보
- 작업 단위 메모리 상한 제어
- 반복 실험 속도 개선

---

## Insight

대규모 워크로드에서는 연산량보다 분할 전략과 데이터 흐름 설계가 확장성을 결정한다.

메모리 상한을 명확히 제한하면 예측 가능한 성능 특성을 확보할 수 있다.
