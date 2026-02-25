---
layout: project
title: "위성 데이터센터 입지 분석 - 분산 지리 연산 파이프라인"
image: /assets/img/projects/Tamna-eye_mainpage.png
---

## Overview
ERA5(zarr) 기반 대용량 지리/기상 데이터를 활용해 후보 지역을 스코어링하는 분산 처리 파이프라인입니다. 단일 알고리즘 최적화보다 메모리 안전성과 데이터플로우 설계를 통해 확장 가능한 실행을 만드는 데 초점을 두었습니다.

## Problem
ERA5 데이터는 크기가 커서 단순 in-memory 방식으로 처리하기 어렵습니다.
- 단일 머신 실행은 느리고 메모리 부담이 큼
- 넓은 범위 로딩 시 I/O 및 메모리 풋프린트가 급증
- 반복 실험 속도가 I/O/aggregation 병목에 의해 제한

## Diagnosis
병목은 알고리즘보다 **데이터 볼륨과 메모리 동작**에 의해 결정되었습니다.
- 지리 집계 과정에서 intermediate array가 크게 생성
- 큰 bounding box가 불필요한 I/O/compute를 유발
- partitioning 부재로 작업 편차와 메모리 스파이크 발생

## Approach
### Tile-based partitioning
- 타일 단위로 분할해 task별 메모리 상한을 고정
- 점진적 집계 및 캐시가 가능하도록 설계

### Distributed execution (AWS Batch + S3)
- 타일 작업을 병렬 job으로 실행
- 중간 산출물을 S3에 저장해 재현성과 재처리 성능 확보

### Scoring abstraction
- node-level scoring 구조로 feature 확장이 쉬운 형태로 분리
- 향후 가속기/추가 데이터 소스 연동을 고려한 모듈화

## Result
- 타일 단위 메모리 상한이 있는 병렬 실행 모델 확보
- S3-backed 중간 산출물로 반복 실험 속도 개선
- 더 넓은 지역/추가 피처로 확장 가능한 기반 마련

## 이미지
![Tamna 메인]({{ '/assets/img/projects/Tamna-eye_mainpage.png' | relative_url }})
![Tamna 솔루션]({{ '/assets/img/projects/Tamna-eye_solution.png' | relative_url }})
![Tamna 발표]({{ '/assets/img/projects/Tamna-eye_presentation.PNG' | relative_url }})
![Tamna 제주 포럼]({{ '/assets/img/projects/Tamna-eye_Jeju global space_forum.jpeg' | relative_url }})
![Tamna 단체샷]({{ '/assets/img/projects/Tamna-eye_단체샷.JPG' | relative_url }})
![Tamna 추가]({{ '/assets/img/projects/Tamna-eye_┤?├??ª.JPG' | relative_url }})

## Key insight
대규모 지리 데이터에서는 partitioning과 데이터플로우 설계가 성능과 확장성을 좌우합니다. task별 메모리 상한을 명확히 하고 compute/storage를 분리하면 복잡한 최적화 알고리즘 없이도 안정적인 확장이 가능합니다.
