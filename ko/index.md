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

### AI Image Analysis — Memory-Bound 추론 최적화  
NVIDIA A100 환경에서 attention-heavy 추론을 프로파일링 및 roofline 관점으로 분석하여 bandwidth-bound 특성을 확인.  
모델 용량 증가 없이 Peak VRAM ~38–40% 감소, End-to-end latency ~22% 개선.  
[**프로젝트 보기 →**]({{ "/ko/projects/01-ai-image-analysis" | relative_url }})

---

### SHPB Calibration — 실험 기반 모델 보정 및 검증  
Split Hopkinson Pressure Bar(SHPB) 실험으로 고변형률 재료 거동을 계측.  
실험 stress-strain 곡선 기반 파라미터 보정으로 동적 하중 조건에서 해석 정확도를 개선.  
[**프로젝트 보기 →**]({{ "/ko/projects/11-shpb-ko" | relative_url }})

---

### OneTakeStudio — Compute-Isolated AI 추론 시스템  
스트리밍 경로와 GPU 기반 추론 워커를 분리하는 아키텍처로 재설계.  
동시 요청 환경에서 blocking 약 35% 감소 및 latency variance 안정화.  
[**프로젝트 보기 →**]({{ "/ko/projects/02-onetakestudio" | relative_url }})

---

### Satellite Data Center Siting — 분할 기반 대규모 연산 설계  
ERA5 위성 데이터를 타일 단위로 분할하고 AWS Batch + S3 기반 분산 파이프라인 구축.  
작업 단위 메모리 상한을 고정해 확장성과 반복 실험 속도 개선.  
[**프로젝트 보기 →**]({{ "/ko/projects/03-aws-dc-siting" | relative_url }})

---

## Engineering Philosophy

성능의 상한은 모델이 아니라 제약 조건에 의해 결정됩니다.

저는 다음을 우선합니다:
- 최적화 전에 측정
- 미세 조정보다 아키텍처 격리
- 단순 스케일링보다 하드웨어 정렬된 실행 설계
