---
layout: project
title: AI 기반 CRM 서비스 제작 (SSAFY)
summary: "고객 로그/구매 이력으로 세그먼트를 정의하고 전환 가능성을 예측, LLM로 메시지/스크립트 생성까지 연결"
title_en: "AI-based CRM Service Development (SSAFY)"
summary_en: "Defined segments from customer logs/purchase history, predicted conversion potential, and connected outputs to LLM-based scripts/messages."
period: "2025–2026"
role: "AI · Data"
stack: "Python, pandas, (추천/분류 모델), LLM 활용"
image: /assets/img/projects/crm_mainpage.png
order: 10
featured: true
links:
  - label: "Repository"
    url: "https://github.com/BeusmKim/REPO"
---

## Overview
데이터 마케팅의 핵심은 “분석 결과”가 아니라 **전환을 만드는 실행 단위**입니다.  
고객 로그/구매 이력을 기반으로 세그먼트를 정의하고, 고객의 관심/전환 가능성을 예측해 타깃팅 시나리오를 설계했습니다.

## Problem
- 고객 데이터는 있으나, “누구에게 무엇을 제안할지”가 실행 단위로 연결되지 않는 문제
- 상담/프로모션 메시지 작성이 담당자 역량에 의존해 품질 편차가 발생

## Approach
- 고객 로그와 구매 이력으로 세그먼트 정의(최근 구매·재구매 가능 고객 등 우선 타깃 설정)
- 고객 관심 상품/전환 가능성을 예측하는 모델(추천/분류)을 구축하고 영업 시나리오로 연결
- LLM을 활용해 고객 유형별 상담 스크립트 및 프로모션 메시지를 자동 생성  
  → “분석 → 실행” 사이의 마찰 비용을 줄이는 방향으로 설계

## Screenshots
![CRM Main Page]({{ '/assets/img/projects/crm_mainpage.png' | relative_url }})
![CRM Session Detail]({{ '/assets/img/projects/crm_session_detail.png' | relative_url }})
![CRM Customer Detail]({{ '/assets/img/projects/crm_customer_detail.png' | relative_url }})
![CRM Recommended]({{ '/assets/img/projects/crm_recommended.png' | relative_url }})
![CRM Recommended Scripts]({{ '/assets/img/projects/crm_recommended_scripts.png' | relative_url }})

## Result
- 세그먼트 기반 타깃팅/추천/메시지 생성이 연결된 CRM 기능 프로토타입 구현
- 데이터 분석이 실제 영업 실행으로 이어지도록 기능 흐름을 제품 관점으로 정리

## Learnings
- 성능보다 중요한 것은 “사용자가 바로 쓸 수 있는 형태(워크플로우)”로 결과를 포장하는 것
