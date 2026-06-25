---
title: 포트폴리오
icon: fas fa-briefcase
order: 5
toc: true
---

> 직접 기획·개발한 프로젝트들을 모바일 앱과 웹으로 나누어 정리했습니다.
> 각 프로젝트는 **핵심 기능**과 **트러블슈팅** 위주로 요약했습니다.
{: .prompt-tip }

---

## 📱 모바일 앱

### FuelKeeper

> 내 주변 주유소 가격 비교 · 주유 가계부 · 전국 유가 통계를 하나의 앱에서
> *Flutter 기반 1인 운전자용 모바일 앱*

**개발 기간** 2026.04.23 ~ 2026.05.01 · **역할** 1인 풀 개발 (기획·디자인·개발·배포)
**기술 스택** Flutter · Dart · Riverpod · go_router · Hive · Naver Map · geolocator · Opinet / Kakao Local API

**주요 기능**

- 내 주변 주유소 **실시간 가격 비교** — GPS 위치 + 반경(1·3·5·10km) + 연료 4종 분리
- **브랜드 컬러 마커 지도** + 나침반 기반 회전 화살표 위치 마커
- **주유 가계부** — 단가×리터·연비 자동 계산, 다차량 지원, CSV 백업/복원
- **전국 통계** — 17개 시·도 평균 + 저가 TOP 10 (외부 차트 0개, CustomPainter 직접 구현)
- 로컬 푸시 알림, 다크모드 · 접근성(Dynamic Type·색맹 보강) 지원

**트러블슈팅**

- **APK 용량 61% 감축 (139MB → 54MB)** — Gradle `jniLibs.excludes` + R8 + 폰트 서브셋팅
- **지도 마커 race condition 해결** — Set diff 갱신 + mutex 직렬화 + 가시성 게이트
- **Hive 손상 자가복구** — 손상 파일 격리(rename) 후 재오픈으로 부팅 100% 보장

**링크** · [GitHub](https://github.com/secgyu)

---

### FitAI

> AI가 만들어주는 나만의 맞춤 운동 루틴
> *GPT-4o-mini 기반 AI 피트니스 플랫폼 (모바일 앱 + 웹 어드민 풀스택)*

**개발 기간** 2026.04.07 ~ 2026.04.11 · **역할** 풀스택 개발
**기술 스택** React Native (Expo) · Next.js 16 · TypeScript · Firebase (Auth·Firestore·Storage) · OpenAI GPT-4o-mini · ExerciseDB API

**주요 기능**

- **AI 운동 루틴 생성** — 프로필(목표·체력·환경·장비) 기반 맞춤 루틴, JSON Schema 구조화 응답
- **운동 세션 기록** — 세트/무게/횟수 입력, 휴식 타이머, ExerciseDB 1300+ 운동 연동
- **기록 & 분석** — 캘린더, 주간 운동량 차트, 진행 추이 분석, 무드 트래킹
- **소셜 커뮤니티** — 게시글 CRUD, 댓글·좋아요·팔로우, AI 채팅 어시스턴트
- **웹 어드민** — 유저/콘텐츠 관리, 신고 처리, 14일 트렌드 분석 대시보드

**트러블슈팅**

- **인증 기반 스마트 리다이렉트** — `authReady` + `onboardingDone` 2중 상태로 깜빡임 제거
- **OpenAI 응답 안정화** — `json_object` 강제 + 스키마 명시 + 프로필 영문 매핑
- **ExerciseDB 최적화** — Map 캐시(TTL 30분) + 페이지네이션 + 검색어 자동 변형

**링크** · [GitHub](https://github.com/secgyu)

---

## 🌐 웹 프로젝트

### SIMVEX

> 공학 구조물을 외우지 않고, 3D로 이해하다
> *3D 인터랙티브 학습 플랫폼 (팀 6명, 프론트엔드 단독)*

**개발 기간** 2026.02.01 ~ 2026.02.11 · **역할** 프론트엔드 개발 (단독)
**기술 스택** React · Three.js · React Three Fiber · Zustand · React Query · Tailwind · Radix UI

**주요 기능**

- **3D 모델 뷰어** — GLB 자동 로딩, OrbitControls 회전, 분해 애니메이션, 부품 하이라이트
- **AI 학습 어시스턴트** — 부품 상세 설명, 실시간 스트리밍 질의응답
- **퀴즈 & 학습 도구** — 객관식/주관식, 개인 메모, PDF 다운로드, 진행률 추적
- **부품 탐색 시스템** — 계층 구조 목록, 마크다운 렌더링, 무한 스크롤

**트러블슈팅**

- **분해(Explode) 애니메이션** — 부품별 방향·거리 메타데이터 + 슬라이더 선형 보간
- **Canvas 내외부 상태 동기화** — Zustand 외부 스토어 + Selector 구독으로 렌더링 최적화

**링크** · [GitHub](https://github.com/secgyu)

---

### 트래비

> 대화 한마디로 완벽한 여행 계획을 세우세요
> *AI 기반 여행 플래너*

**개발 기간** 2025.11.07 ~ 2026.01.16 · **역할** 프론트엔드 개발
**기술 스택** Next.js 16 · React 19 · TypeScript · Supabase · NextAuth · OpenAI GPT-4o-mini · Vercel AI SDK · Google Maps

**주요 기능**

- **AI 일정 생성** — "3박4일 도쿄 여행 일정 만들어줘" 한마디로 맞춤 일정 자동 생성
- **지도 시각화** — Google Maps 동선 확인, 순서가 보이는 커스텀 숫자 마커
- **대화형 수정** — 자연스러운 대화로 일정 수정, PDF 저장

**트러블슈팅**

- **AI 응답 구조화** — 프롬프트 예시 명시 + 정규식 하이브리드 파싱으로 95%+ 성공률
- **스마트 지오코딩** — 영문명+도시명 → OpenAI → 도시 중심 3단계 폴백 (API 70% 절감)
- **Google Maps 커스텀 마커** — `AdvancedMarkerElement` + DOM으로 자유 스타일링
- **클라이언트 PDF 생성** — `html2canvas` + `jsPDF`로 서버 비용 0원, 한글·이모지 정상 출력

**링크** · [GitHub](https://github.com/secgyu)

---

### SEESAW

> Different is Balance
> *프리미엄 패션 브랜드 이커머스 (1인 풀스택)*

**개발 기간** 2025.12.02 ~ 2025.12.16 · **역할** 1인 풀스택 개발
**기술 스택** Next.js 16 · React 19 · TypeScript · Tailwind · Framer Motion · Supabase · Stripe · Resend

**주요 기능**

- **쇼핑** — 제품 목록/상세/검색/필터, 장바구니·위시리스트(DB 연동), 최근 본 상품
- **결제** — Stripe Checkout, 쿠폰/할인 코드, 주문 확인 이메일(Resend)
- **인증** — 로그인/회원가입, 비밀번호 재설정, 프로필·계정 관리
- **관리자** — 매출/주문 통계 대시보드, 주문·상품·재고·쿠폰 관리

**트러블슈팅**

- **Stripe 결제 상태 동기화** — Webhook `checkout.session.completed` 서버 처리로 누락 0건
- **동적 쿠폰 할인** — 결제 시점 일회용 Stripe Coupon 동적 생성으로 자체 쿠폰 연동
- **프리미엄 UX** — Framer Motion 애니메이션 + Quick View 모달 + 다크모드 무드

**링크** · [GitHub](https://github.com/secgyu)

---

### Business Warning System

> AI 기반 자영업 위험도 진단 플랫폼
> *데이터 분석 기반 맞춤형 경영 개선 솔루션 (빅콘테스트)*

**개발 기간** 2025.09 ~ 2025.12 · **역할** 프론트엔드 개발
**기술 스택** React 19 · TypeScript · TanStack Query · Zustand · Tailwind · Radix UI · FastAPI · SQLAlchemy · Pandas

**주요 기능**

- **AI 진단** — 매출/고객/시장 리스크 분석
- **벤치마크** — 업종별 평균 비교 분석
- **실행 계획** — 개선 액션 아이템 관리
- **인사이트** — 트렌드 및 AI 챗봇

**트러블슈팅**

- **장바구니 로컬/DB 동기화** — 비로그인 localStorage → 로그인 시 DB 자동 마이그레이션
- **Type-Safe API** — `openapi-typescript`로 FastAPI 스펙 → TS 타입 자동 생성, 런타임 에러 제거

**링크** · [GitHub](https://github.com/secgyu)

---

### 학문공유

> 전공 지식을 함께 나누는 학습 커뮤니티
> *전공 공유 플랫폼*

**개발 기간** 2025.04.29 ~ 2025.05.20 · **역할** 프론트엔드 개발 (4인 팀)
**기술 스택** React 19 · TypeScript · Tailwind · React Query · Zustand · Zod · Node.js · Express · MongoDB

**주요 기능**

- **문제 공유/관리** — CRUD, 전공/태그별 필터링, 파일 첨부
- **마크다운 에디터 + 수식** — KaTeX 기반 수학 수식 렌더링
- **댓글/대댓글 + AI 답변** — 중첩 댓글, 좋아요, AI 추천 답변
- **사용자 랭킹 시스템** — 기여도/해결 문제 기반 랭킹, 활동 통계

**트러블슈팅**

- **마크다운 + KaTeX 실시간 렌더링** — `remark-math` + `rehype-katex`, CSR로 hydration 오류 해결 (번들 100KB 미만)
- **중첩 댓글 시스템** — 단일 `replyingTo` 상태로 토글 관리 + React Query 캐시 무효화

**링크** · [GitHub](https://github.com/secgyu)

---

> 각 프로젝트의 **GitHub·데모 링크**는 실제 저장소 주소로 교체하면 됩니다.
{: .prompt-info }
