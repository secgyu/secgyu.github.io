---
title: FuelKeeper
description: 내 주변 주유소 가격 비교 · 주유 가계부 · 전국 유가 통계를 하나의 앱에서
date: 2026-05-01 18:00:00 +0900
categories: [포트폴리오, 앱]
tags: [Flutter, Dart, Riverpod, Hive, NaverMap]
---

> Flutter 기반 1인 운전자용 모바일 앱
{: .prompt-tip }

**개발 기간** 2026.04.23 ~ 2026.05.01
**역할** 1인 풀 개발 (기획 · 디자인 · 개발 · 배포)
**배포** Android arm64 APK (54MB)

## 프로젝트 개요

### 기획 배경

운전자가 매번 "어디 주유소가 싸지?"를 검색하면서도, 정작 본인이 그동안 얼마를 썼고 연비가 어떤지는 모르는 문제가 있었습니다. 기존 앱은 가격 비교만, 가계부 앱은 기록만 제공해 두 흐름이 끊겨 있었습니다.

### 솔루션

- 실시간 가격 비교 + 개인 주유 가계부를 **한 앱으로**
- Hive 기반 로컬 가계부 → 가입·로그인 없이 즉시 사용
- 전국 시·도 평균 + 저가 TOP 10으로 거시 트렌드까지 제공

## 기술 스택

| 분류 | 사용 기술 |
|------|-----------|
| Framework | Flutter 3.x · Dart 3.x |
| State / Routing | Riverpod 3.x · go_router 17 |
| Storage | Hive · SharedPreferences · 30분 인메모리 캐시 |
| Map / Location | flutter_naver_map · geolocator · flutter_compass · proj4dart |
| External API | Opinet 유가정보 · Naver Cloud Maps · Kakao Local |

아키텍처는 **Clean Architecture 4-Layer**(Presentation → Application → Domain → Data)로 구성했고, 차트는 외부 라이브러리 없이 **CustomPainter로 직접 구현**했습니다. Repository를 추상화해 `--dart-define=USE_MOCK=true`로 Mock/실데이터를 즉시 전환할 수 있습니다.

## 주요 기능

- **내 주변 가격 비교** — GPS 자동 위치 + Kakao 역지오코딩, 반경 1/3/5/10km, 연료 4종 분리
- **브랜드 컬러 마커 지도** — Naver Map 가격 캡션 마커, 줌 기반 클러스터링, 나침반 회전 화살표 마커
- **주유 로그** — 단가×리터 총액·연비 자동 계산, 월별 그룹핑, GPS 자동 매칭, 다차량 지원
- **CSV 내보내기/가져오기** — 백업·기기 이전·엑셀 분석
- **전국 통계** — 17개 시·도 평균 막대 차트, 시·도별 저가 TOP 10
- **알림·접근성** — 로컬 푸시, 다크모드(Material 3), Dynamic Type, 색맹 보강

## 트러블슈팅

### 1. APK 사이즈 최적화 — 139MB → 54MB (-61%)

Universal APK가 139MB로 권장치를 초과했습니다. `--target-platform android-arm64`만으로는 외부 패키지의 prebuild `.so`가 모든 ABI를 포함해 100.8MB까지밖에 줄지 않았습니다.

- arm64 단일 빌드로 Flutter 엔진 ABI 단일화
- Gradle `packaging.jniLibs.excludes`로 `armeabi-v7a` 차단
- R8 + `shrinkResources`로 미사용 코드/리소스 제거
- 폰트 서브셋팅으로 한글 폰트 용량 축소

> Flutter `--target-platform`은 엔진 ABI만 제한한다. 외부 패키지 native lib는 Gradle 레이어에서 직접 걸러야 한다.
{: .prompt-info }

### 2. 지도 마커 재드로우 직렬화 + 클러스터 보존

`clearOverlays()` → `addOverlay()` 패턴이 클러스터 매니저 내부 상태와 충돌해, 빠른 연속 호출 시 마커가 사라지거나 중복되는 race condition이 발생했습니다.

- 현재 마커 ID를 `Set<String>`으로 추적, 차집합 diff로 추가/삭제만 개별 호출
- 모든 마커 작업을 단일 mutex로 직렬화
- `WidgetsBindingObserver` + `RouteAware`로 visible일 때만 재드로우

### 3. Hive Box 손상 자가복구

파일 손상 시 `openBox()`가 throw되어 스플래시에서 멈추고, 단순 `deleteFromDisk()`는 데이터를 전부 날리는 비가역 처리였습니다.

- 모든 Box 오픈을 `openBoxResilient<T>()`로 일원화
- 손상 시 `*.corrupted.<ts>.hive`로 격리(rename) 후 새 Box 정상 오픈
- 앱은 항상 부팅 성공, 격리 파일은 사후 분석용 보존

## 배운 점

- 빌드 시스템을 끝까지 파고들어야 외부 native lib까지 제어할 수 있다
- 외부 SDK 상태를 존중하는 diff + 직렬화 + 가시성 게이트
- "실패해도 괜찮은" 방어적 프로그래밍 (비가역 삭제는 마지막 수단)
- CustomPainter로 차트 라이브러리 0개, 디자인 100% 컨트롤
