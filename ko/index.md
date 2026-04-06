---
layout: default
title: Home
permalink: /ko/
---

# 김범수
### AI 엔지니어 — 물리 시스템 모델링, 학습 기반 제어 & 온디바이스 AI

물리 시스템의 동적 거동을 실험으로 계측하고, 실측 데이터를 기반으로 모델을 보정하며,  
실제 하드웨어 제약 하에서 학습 기반 시스템을 훈련합니다.

고변형률 재료 특성화(SHPB, Abaqus FEM)부터 대형 VLM 파인튜닝(LoRA, 양자화),  
온디바이스 AI 파이프라인 설계까지 — 모든 단계에서 측정 기반 검증을 중심에 둡니다.

---

## Core Competencies

- 물리 시스템 특성화 및 구성 모델 보정 (SHPB, FEM)
- 실험 방법론: measure → model → calibrate → validate
- GPU 제약 하 대형 VLM 파인튜닝 (LoRA, INT8 양자화, 앙상블)
- 온디바이스 AI 시스템 설계 (양자화 ASR, 슬롯 기반 LLM 에이전트)
- 하드웨어 제약 기반 추론 최적화 (FP16 / INT8, CUDA 인지형 실행)

---

## 대표 프로젝트

### SHPB Calibration — 고변형률 재료 특성화 & 모델 검증  
Split Hopkinson Pressure Bar(SHPB) 실험으로 동적 재료 거동을 계측하고, 실험 stress-strain 곡선을 기반으로 구성 모델 파라미터를 보정.  
Abaqus FEM 시뮬레이션으로 검증 — 제어공학의 시스템 식별과 동일한 measure → model → calibrate → validate 워크플로우 적용.

[**프로젝트 보기 →**]({{ "/ko/projects/11-shpb-ko" | relative_url }})

---

### DailyLog — 온디바이스 음성 AI 파이프라인 & 적응형 추천 시스템
🏆 우수상 — SSAFY 특화 프로젝트 (2026)
int8 양자화 온디바이스 ASR(~300ms), 슬롯 기반 LLM 에이전트 일기 자동생성, 톰슨 샘플링 추천 엔진을 연결한 음성 일기 시스템.
일기 작성 시간 약 20분 → 5분으로 약 70% 단축.

[**프로젝트 보기 →**]({{ "/ko/projects/12-dailylog" | relative_url }})

---

### VQA 파인튜닝 — Qwen3-VL LoRA 학습 & 앙상블  
VQA 대회 데이터셋에서 Qwen3-VL-8B-Instruct를 LoRA로 파인튜닝, Baseline 0.76에서 Public Score 0.96까지 개선.  
모델 교체, BLIP 캡션 증강 실험, 3가지 LoRA 설정 하이퍼파라미터 탐색, 로지스틱 회귀 앙상블을 통해 최종 **0.96759** 달성.

[**프로젝트 보기 →**]({{ "/ko/projects/09-vqa-qwen" | relative_url }})

---

## Engineering Philosophy

성능의 상한은 모델이 아니라 제약 조건이 결정합니다.

- 최적화 전에 측정
- 미세 조정보다 구조적 격리
- 단순 스케일링보다 하드웨어 특성에 맞춘 실행 설계
