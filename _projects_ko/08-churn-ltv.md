---
layout: project
title: "Churn × LTV — Decision-Oriented Segmentation"
summary: "ARPU 중심 접근의 한계를 보완해 다중변수 기반 LTV 모델을 설계하고, 이탈 위험군 분류 및 전환 전략을 제안"
title_en: "Telecom Customer LTV Improvement and Churn Prediction"
summary_en: "Built a multivariate LTV model beyond ARPU-only assumptions, classified churn risk groups, and proposed conversion actions."
period: "2025–2026"
role: "Data Analyst"
stack: "Python, pandas, scikit-learn, Regression/Classification"
image: /assets/img/projects/churn-ltv.jpg
order: 990
featured: false
links:
  - label: "Repository"
    url: "https://github.com/BeusmKim/REPO"
---

## Overview
고객 이탈(Churn)과 LTV를 예측하고, 실제 운영에서 활용 가능한 액션 후보를 도출하는 분석/모델링 프로젝트입니다. 단순 예측 성능보다 “어떤 고객을 왜 우선 대응해야 하는지”를 설명 가능한 형태로 만드는 것을 목표로 했습니다.

## Problem
운영 관점에서 이탈 대응은 다음 문제를 갖습니다.
- 모든 고객을 동일하게 케어할 수 없어 우선순위가 필요
- 단순 이탈 확률만으로는 비용 대비 효율이 나오지 않을 수 있음(LTV 고려 필요)
- 예측이 맞더라도 액션으로 연결되지 않으면 의미가 없음

## Diagnosis
병목은 예측 그 자체보다 “의사결정 가능한 신호”와 “우선순위 규칙”의 부재였습니다.
- Churn probability와 LTV를 분리해서 보면 현장 우선순위가 뒤틀릴 수 있음
- 지표가 설명되지 않으면 운영팀이 신뢰하거나 실행하기 어렵음
- cohort/segment 별로 이탈 요인이 다르면 단일 정책이 비효율적

## Approach
### Churn × LTV 기반 우선순위 프레임
- 이탈 위험과 기대 가치(LTV)를 함께 고려해 타깃팅 우선순위를 정의
- “High risk × High value”를 최우선 대응군으로 설정

### 세그먼트 기반 해석
- 고객을 세그먼트로 나누고, 구간별 특성을 비교
- 운영 시나리오에서 활용 가능한 요인 해석(설명)을 함께 제공

### 실행 중심 산출물
- 운영팀이 바로 사용할 수 있는 타깃 리스트/규칙 형태로 결과를 정리
- 우선순위별 추천 액션을 연결(예: 유지 프로모션, 상담, 혜택 제공 등)

## Result
- 이탈 위험과 가치(LTV)를 결합한 우선순위 산정 체계를 구축
- 예측 결과를 운영 의사결정과 연결 가능한 형태로 구조화

## Key insight
예측 프로젝트의 완성은 점수(accuracy) 자체가 아니라, 운영에서 “누구에게 무엇을 할지”를 결정할 수 있게 만드는 구조(우선순위, 설명, 액션 연결)입니다.
