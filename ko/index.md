---
layout: default
title: Home
permalink: /ko/
---

# 김범수
### 하드웨어 제약 기반 AI 시스템 엔지니어 (CUDA · FP16/INT8 · Memory/Latency)

저는 실제 하드웨어 제약 환경에서 AI 모델 실행 병목을 진단하고,  
compute-bound인지 memory-bandwidth bound인지 구분한 뒤 실행 경로를 재설계하는 방식으로 성능을 개선합니다.

모델을 키우는 대신, 정밀도 전략·텐서 생명주기·아키텍처 구조를 조정해  
측정 가능한 런타임 개선을 만드는 데 집중합니다.

---

## Core Competencies

- Attention-heavy transformer의 memory-bound 특성 진단
- Mixed precision 및 quantization(FP16 / INT8) 트레이드오프 설계
- CUDA 인지형 실행 구조 및 동시성 안정화
- Latency-sensitive 시스템을 위한 compute isolation 아키텍처
- 메모리 상한을 제어하는 분할 기반 대규모 연산 설계

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

성능의 상한은 모델이 아니라 제약 조건에 의해 결정됩니다.

저는 다음을 우선합니다:
- 최적화 전에 측정
- 미세 조정보다 아키텍처 격리
- 단순 스케일링보다 하드웨어 정렬된 실행 설계
