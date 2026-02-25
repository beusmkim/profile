---
layout: default
title: Home
permalink: /ko/
---

# 김범수
### 하드웨어 인지형 AI 시스템 엔지니어 (CUDA · FP16/INT8 · Memory/Latency)

저는 AI 모델 실행을 하드웨어 제약에 맞추어 최적화하는 데 집중합니다. 특히 메모리 대역폭, VRAM 풋프린트, 런타임 동작(동시성/격리)에 의해 성능이 결정되는 구간에서 안정적이고 재현 가능한 개선을 만드는 것을 목표로 합니다.

## 제가 최적화하는 영역
- attention-heavy transformer 실행의 memory-bound 특성 진단 및 개선
- precision/deployment 트레이드오프(FP16, INT8) 설계
- 동시성 환경에서의 GPU 활용률/지연(variance) 안정화
- 추론 시스템 아키텍처(격리, 워커 오케스트레이션, 분산 처리)

## Featured work (AI silicon / runtime 최적화 관점 우선)
- AI Image Analysis — Memory-Bound Inference Optimization  
  FP16로 peak VRAM ~38–40% 감소, INT8 탐색으로 latency ~22% 개선, CUDA 인지형 개선으로 제한된 GPU 환경에서 안정성 향상.  
  [View project]({{ "/ko/projects/01-ai-image-analysis" | relative_url }})

- OneTakeStudio — Compute-Isolated AI Inference System  
  스트리밍 경로와 추론 워커를 분리하여 자원 경합을 줄이고 동시 요청 blocking ~35% 감소.  
  [View project]({{ "/ko/projects/02-onetakestudio" | relative_url }})

- Satellite Data Center Siting — Distributed Geospatial Compute  
  ERA5(zarr) 대용량 지리/기상 데이터를 타일 기반으로 분할하고 AWS Batch/S3로 수평 확장 가능한 파이프라인 구축.  
  [View project]({{ "/ko/projects/03-aws-dc-siting" | relative_url }})

