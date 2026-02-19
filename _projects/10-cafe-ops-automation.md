---
layout: project
title: 카페 운영 자동화 — 원가/재고/매출 관리의 통합
summary: "엑셀 수작업 운영을 자동화하는 프로그램을 설계·구현해 일일 업무를 30분 → 5분 이내로 단축"
title_en: "Cafe Operations Automation for Cost/Inventory/Sales"
summary_en: "Designed and implemented automation to replace manual spreadsheet operations, reducing daily work from 30 minutes to under 5 minutes."
period: "2026"
role: "Product Planner · Builder"
stack: "Requirements, Data Modeling, Automation, (LLM assisted)"
image: /assets/img/projects/cafe-automation.jpg
order: 1000
featured: false
---

## Problem
카페 운영자가 원가/재고/매출을 매일 엑셀에 수작업 입력하면서 누락/오류가 잦고 시간이 많이 소요되었습니다.  
데이터가 분리되어 있어 메뉴 변경 시 연동도 어렵다는 문제가 있었습니다.

## Approach
- 요구사항(원가·재고·매출 연동)을 빠르게 구조화하고 데이터 흐름을 설계
- 메뉴 변경 시 자동 반영, 재고 자동 차감, 매출 집계가 한 번에 되도록 계산 로직을 통합
- 모바일에서도 확인/입력이 쉬운 단순 UI를 지향(프로토타입 설계)

## Result
- 일일 관리 업무 시간 **30분 이상 → 5분 이내**로 단축
- 입력 오류/누락이 크게 감소

## Learnings
- AI 도구(요구사항 정리/코드/UX 아이디어)를 “역할 분담”해 활용하면 개발 속도와 완성도를 함께 올릴 수 있음
