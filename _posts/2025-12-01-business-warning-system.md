---
title: Business Warning System
description: AI 기반 자영업 위험도 진단 플랫폼 — 데이터 분석 기반 경영 개선 솔루션
date: 2025-12-01 18:00:00 +0900
categories: [포트폴리오, 웹]
tags: [React, FastAPI, TanStackQuery, Pandas, TypeScript]
---

> AI 기반 자영업 위험도 진단 플랫폼 (빅콘테스트 데이터 활용)
{: .prompt-tip }

**개발 기간** 2025.09 ~ 2025.12 (주 2회 평균 3시간)
**역할** 프론트엔드 개발

## 기술 스택

| 분류 | 사용 기술 |
|------|-----------|
| Frontend | React 19 · TypeScript · TanStack Query · Zustand · Tailwind · Radix UI · openapi-ts |
| Backend | FastAPI · FastAPI Users(JWT) · SQLAlchemy · Pandas (86K 레코드 분석) |
| Architecture | Feature-based(FE) · Layered Router-Service-Model(BE) |

## 주요 기능

- **AI 진단** — 매출/고객/시장 리스크 분석
- **벤치마크** — 업종별 평균 비교 분석
- **실행 계획** — 개선 액션 아이템 관리
- **인사이트** — 트렌드 및 AI 챗봇

## 트러블슈팅

### 1. 장바구니 로컬/DB 동기화

비로그인 사용자도 장바구니를 쓰고, 로그인 시 기존 데이터가 유실되면 안 됐습니다.

- 비로그인: localStorage 저장
- 로그인 시: localStorage → Supabase DB 자동 마이그레이션 후 localStorage 삭제(중복 방지)

### 2. Type-Safe API Integration

백엔드 스펙 변경 시 프론트 타입 불일치로 런타임 에러가 발생하고, 수동 타입 관리는 휴먼 에러가 많았습니다.

- FastAPI의 OpenAPI 스펙에서 `openapi-typescript`로 TS 타입 자동 생성
- `npm run generate-types` 원클릭 업데이트 → 컴파일 타임 검증, **API 타입 에러 100% 제거**

## 배운 점

- Contract-Driven Development와 DX 개선의 중요성
- Feature-based 아키텍처를 통한 대규모 프로젝트 구조화
- 클라이언트/서버 상태 분리와 데이터 일관성 유지 전략
