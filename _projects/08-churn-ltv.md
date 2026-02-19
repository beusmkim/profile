---
layout: project
title: 이통사 고객 LTV 모델 개선 & 이탈 예측
summary: "ARPU 중심 접근의 한계를 보완해 다중변수 기반 LTV 모델을 설계하고, 이탈 위험군 분류 및 전환 전략을 제안"
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
통신 서비스는 가격/사용 패턴/결합 여부 등 요인이 복합적으로 작동합니다.  
단일 지표(ARPU) 중심의 예측은 설명력에 한계가 있어, 요금제·데이터 사용·결합·부가서비스 이용 등 변수를 반영한 LTV 모델을 설계했습니다.

## Problem
- ARPU 중심 모델은 고객 가치의 원인을 설명하기 어렵고, 실행 전략으로 연결되기 어려움
- 이탈은 “발생 후 대응”보다 **위험 신호를 조기에 탐지**하는 체계가 필요

## Approach
- 요금제/데이터 사용 패턴/결합/부가서비스 등 변수를 반영한 다중회귀 기반 LTV 모델 설계 및 유효성 검증
- 이탈 고객 특성을 분석해 위험군을 분류하고, 위험 신호 발생 시 적용할 전환 전략을 제안
- 결과를 “분석 보고”가 아닌 “실행 플레이북” 형태로 정리

## Result
- LTV 예측과 이탈 위험군 분류를 통해 타깃팅 우선순위 및 전환 액션을 제안 가능한 형태로 구성

## Limitation & Next
- 시뮬레이션 데이터 기반이라 이벤트성 이탈 등 외생 변수를 충분히 반영하지 못함  
  → 실제 운영 데이터로 확장 시, 정책/이벤트 피처 반영 및 온라인 모니터링 체계 보완 예정
