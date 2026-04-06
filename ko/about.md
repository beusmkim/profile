---
layout: default
title: About
permalink: /ko/about
---

# About

물리 시스템의 동적 거동을 실험으로 계측하고, 실측 데이터를 기반으로 모델을 보정하며, 실제 하드웨어 제약 하에서 학습 기반 시스템을 훈련합니다.

고변형률 재료 특성화(SHPB, Abaqus FEM)부터 대형 VLM 파인튜닝(LoRA, 양자화), 온디바이스 AI 파이프라인 설계까지 — 모든 단계에서 측정 기반 검증을 원칙으로 삼습니다.

---

## Core Capabilities

- 물리 시스템 특성화 및 구성 모델 보정 (SHPB, Abaqus FEM)
- 실험 방법론: measure → model → calibrate → validate
- GPU 제약 하 대형 VLM 파인튜닝 (LoRA, INT8 양자화, 앙상블)
- 온디바이스 AI 시스템 설계 (양자화 ASR, 슬롯 기반 LLM 에이전트)
- 하드웨어 제약 기반 추론 최적화 (FP16 / INT8, CUDA 인지형 실행)

---

## Technical Stack

### Physical System Modeling
- Split Hopkinson Pressure Bar (SHPB) 실험 설계 및 계측
- 구성 모델 파라미터 보정 (SK material model)
- Abaqus FEM 시뮬레이션 및 실험 검증

### AI & Machine Learning
- Qwen3-VL LoRA 파인튜닝 (rank 16/32, INT8 양자화)
- BLIP 보조 모델 실험 및 앙상블 (Logistic Regression 메타 모델)
- int8 양자화 온디바이스 ASR, 슬롯 기반 LLM 에이전트
- Thompson Sampling 기반 추천 엔진

### Inference Optimization
- Mixed precision 배포 (FP16 / INT8)
- torch.profiler 기반 kernel-level 분석
- Roofline 관점의 memory-bound vs compute-bound 진단
- CUDA 인지형 실행 구조 및 동시성 안정화

---

## Representative Evidence

- SHPB 실험 기반 구성 모델 보정 → Abaqus FEM 시뮬레이션 오차 감소
- VQA Public Score: Baseline 0.76 → 앙상블 최종 **0.96759**
- DailyLog 일기 작성 시간: ~20분 → ~5분 (~70% 단축)
- Peak VRAM ~38–40% 감소, Inference latency ~22% 개선

---

## Engineering Philosophy

성능의 상한은 목표가 아니라 제약 조건이 결정합니다.

- 최적화 전에 측정
- 미세 조정보다 구조적 격리
- 단순 스케일링보다 하드웨어 특성에 맞춘 실행 설계
