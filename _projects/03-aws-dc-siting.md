---
layout: project
title: AWS Hackathon — Distributed Data Center Siting Optimization
summary: "재생에너지/환경 조건을 반영해 최적의 입지 노드 조합을 탐색하는 프로토타입"
period: "2026"
role: "Infra/Data Pipeline"
stack: "AWS (S3, Batch, EC2, IAM), Python, Zarr/Xarray"
image: /assets/img/projects/Tamna-eye_mainpage.png
links:
  - label: "Repository"
    url: "https://github.com/username/REPO"
order: 80
featured: true
---
## Problem
데이터센터 입지 선정은 전력(재생에너지)·냉각(기온/습도)·통신(접근성) 등 복합 조건을 동시에 고려해야 합니다.  
기존의 정적 기준(연평균/단일 관측값)만으로는 계절성·시간대 변동, 특히 풍력 같은 **재생에너지의 변동성(24/7 가용성)**을 반영하기 어렵습니다.

## Satellite Data & Preprocessing (핵심)
### 1) Sentinel-1 Level-2 OCN (Ocean Wind Field)
- 출처: ESA Copernicus 공개 아카이브 기반 Sentinel-1 OCN(해상 풍장) 데이터
- 목적: 제주 인근 해역의 풍속/풍향 시계열 특성을 확보해 풍력 잠재력을 정량화
- 전처리:
  - 품질 플래그/결측/이상치 제거(QC)
  - 공간 좌표 정합(경위도 좌표계) 및 ROI(제주 중심) BBox 컷
  - 시간 축 정리(관측 타임스탬프 표준화)
  - 목표 격자(노드 그리드)에 맞춘 리샘플링/보간
- 활용:
  - 노드별 풍속 통계(평균/분산/상위 퍼센타일) 산출
  - 풍력발전과 연결 가능한 **풍력 잠재력 점수(power proxy score)**로 변환
  - 시간대/계절 변동성을 반영한 안정적 가용성 점수 구성

### 2) GK-2A AMV (Atmospheric Motion Vector)
- 출처: 국가기상위성센터(NMSC) 공개 AMV(대기 바람벡터) 데이터
- 목적: Sentinel-1이 커버하지 못하는 시간/공간 구간 보완 및 대기 흐름 변화 반영
- 전처리:
  - AMV 품질지수 기반 필터링(저품질 벡터 제거)
  - 고도/층 메타데이터 정리
  - 제주 ROI 컷 후 노드 그리드로 리샘플링
- 활용:
  - 해상/연안 풍장 결합으로 풍력 지표의 시간 연속성 확보
  - 급변 시간대/계절 구간을 리스크/안정성 요소로 점수화에 반영

### 3) (보조) ERA5 재분석(기상) — 냉각/보조 풍장
- 출처: 공개 기상 재분석 데이터(ERA5)
- 목적: 기온 기반 냉각 지표 및 풍장 보정/보완
- 전처리/활용:
  - Zarr/GRIB 데이터 로딩 후 제주 ROI 컷 및 월/계절/시간대 집계
  - 냉각 관련 변수(기온 등)를 Cooling Score로 변환
  - 위성 풍장 지표와 결합해 전력(풍력) 점수 안정성 판단 보조

## Approach
- 노드 단위 스코어 정의:
  - `power_score` (풍력 잠재력/가용성)
  - `cooling_score` (기온 기반 냉각 유리성)
  - `network_score` (통신 접근성)
  - (추가로 수요/리스크 등 확장 가능)
- 전처리 파이프라인 분리 설계:
  - 대용량 원천 데이터(위성/재분석) → ROI 컷/보간/집계 → 노드 피처 테이블 변환
  - 결과를 `nodes.json`/Parquet 등으로 내보내 프론트가 즉시 사용 가능하게 구성
- 확장 가능한 실행 구조(AWS 중심):
  - S3에 원천/중간 산출물/최종 노드 데이터 저장
  - AWS Batch 기반 전처리 잡 분리로 스케일아웃 가능하게 설계
- UI(지도 탐색):
  - 사용자가 전력/냉각/통신 가중치를 조절하면 합산 점수가 즉시 업데이트되고 추천 노드 조합 탐색

## Screenshots
![Tamna-eye Main Page]({{ '/assets/img/projects/Tamna-eye_mainpage.png' | relative_url }})
![Tamna-eye Solution]({{ '/assets/img/projects/Tamna-eye_solution.png' | relative_url }})
![Tamna-eye Presentation]({{ '/assets/img/projects/Tamna-eye_presentation.PNG' | relative_url }})
![Tamna-eye Jeju Global Space Forum]({{ '/assets/img/projects/Tamna-eye_Jeju global space_forum.jpeg' | relative_url }})
![Tamna-eye Team Photo]({{ '/assets/img/projects/Tamna-eye_단체샷.JPG' | relative_url }})

## Outcome
- 사용자 입력(가중치) 기반 탐색 UI + 스코어링 로직을 MVP로 구현
- Sentinel-1 OCN, GK-2A AMV(및 ERA5 보조)를 통해 **재생에너지 변동성(시간대/계절성)**을 반영한 입지 점수화를 구성
- 실제 운영 데이터/추가 위성 변수를 연결하면, S3/Batch 중심 구조로 대규모 스케일아웃 가능한 기반 확보
