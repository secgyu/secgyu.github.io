---
title: 학문공유
description: 전공 지식을 함께 나누는 학습 커뮤니티 — 전공 공유 플랫폼
date: 2025-05-20 18:00:00 +0900
categories: [포트폴리오, 웹]
tags: [React, TypeScript, ReactQuery, MongoDB, KaTeX]
---

> 전공 공유 플랫폼 (4인 팀)
{: .prompt-tip }

**개발 기간** 2025.04.29 ~ 2025.05.20 (22일, 매일 5시간)
**역할** 프론트엔드 개발 (4인 팀: BE 2 · FE 2)

## 프로젝트 개요

전공자들을 위한 지식 공유 & 소통 게시판입니다. 자료 업로드, 댓글, 태그 분류, AI 답변 추천 기능을 갖춘 학습 커뮤니티 플랫폼입니다.

**타겟 사용자**: 대학생, 전공 학습자, 학문적 질문이 있는 사용자

## 기술 스택

| 분류 | 사용 기술 |
|------|-----------|
| Frontend | React 19 · TypeScript · Tailwind CSS · React Query · Zustand · Zod |
| Backend | Node.js · Express · MongoDB · JWT |
| Deploy / Tools | Vercel · Heroku · Postman · Swagger |

담당: UI/UX 구현 90% · 상태관리 85% · API 연동 80%. Radix UI 기반 접근성(a11y) 컴포넌트 설계.

## 주요 기능

- **문제 공유/관리** — CRUD, 전공/태그별 필터링, 파일 첨부
- **마크다운 에디터 + 수식** — 마크다운 문법 + KaTeX 수학 수식 렌더링
- **댓글/대댓글 + AI 답변** — 중첩 댓글, 좋아요, AI 추천 답변
- **사용자 랭킹 시스템** — 기여도/해결 문제 기반 랭킹, 활동 통계 시각화

## 트러블슈팅

### 1. 마크다운 + KaTeX 수식 실시간 렌더링

수학 전공 문제에 수식 표현이 필수였지만 일반 에디터는 LaTeX 미지원이고, SSR에서 hydration 오류가 났습니다. MathJax는 번들이 500KB+로 과다했습니다.

- `@uiw/react-md-editor` + `remark-math` + `rehype-katex` 조합
- 클라이언트 사이드 렌더링으로 hydration 오류 해결
- **실시간 미리보기 + 100KB 미만** 번들 달성

### 2. 중첩 댓글(대댓글) 시스템

부모-자식 재귀 구조 설계와 답글 폼 토글 상태 관리가 복잡했습니다.

- 백엔드에서 `replies` 필드로 중첩 구조 반환
- 단일 `replyingTo` 상태 하나로 활성 폼 관리
- React Query 캐시 무효화로 실시간 반영

## 배운 점

- MathJax(500KB) vs KaTeX(26KB) 비교 후 선택 → 번들 분석 습관
- 복잡한 UI 상태도 설계를 단순화하면 관리가 쉬워진다
- Postman 컬렉션 공유로 실시간 API 명세 동기화 (협업)
- hydration 오류 디버깅으로 SSR/CSR 차이 체득
