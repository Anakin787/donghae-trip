# 경주월드 먹거리 가이드 (GYEONGJU WORLD FOOD PASS)

경주월드 내부의 햄버거·카페·분식·푸드트럭 먹거리를 한눈에 볼 수 있는 정적 PWA(Progressive Web App)입니다.
제공된 장소·리뷰 텍스트를 바탕으로 만든 정리용 웹페이지이며, 각 항목은 네이버지도 검색 결과로 연결됩니다.

- **배포**: GitHub Pages — https://anakin787.github.io/gjworld-pwa/
- **저장소**: https://github.com/Anakin787/gjworld-pwa

---

## 기능 스펙

### 콘텐츠
- 경주월드 내부 먹거리 **22곳** 데이터 (가게명, 카테고리, 리뷰 수, 별점, 영업 상태, 위치, 대표 후기, 배지)
- **11개 카테고리**: 전체 / 햄버거 / 카페·디저트 / 카페 / 도시락·컵밥 / 종합분식 / 피자 / 핫도그 / 차·버블티 / 푸드트럭 / 한식
- 상황별 추천 코스 4종 (빨리 든든하게 / 잠깐 쉬어가기 / 놀이기구 전 간식 / 사진 남기기)

### 인터랙션
- **검색**: 가게명·메뉴·후기·카테고리·배지 키워드 통합 검색 (공백 무시, 대소문자 무시)
- **카테고리 필터**: 가로 스크롤 칩, 선택 시 즉시 필터링
- **정렬**: 리뷰 많은 순 기본 정렬
- **표시 개수**: 현재 필터 결과 개수 실시간 표시
- **네이버지도 연결**: 각 카드의 버튼이 `map.naver.com` 검색 결과로 연결
- **인앱 브라우저 폴백**: 카카오톡 등 새 창(`target="_blank"`)을 막는 인앱 브라우저에서 새 창이 차단되면 현재 화면에서 바로 이동

### PWA
- **오프라인 지원**: Service Worker가 앱 셸(HTML·매니페스트·아이콘)을 캐시 우선(cache-first)으로 제공
- **설치 가능**: `beforeinstallprompt` 처리로 "📲 앱으로 설치" 버튼 노출, 홈 화면에 추가 가능
- **매니페스트**: standalone 디스플레이, 192/512 일반 + maskable 아이콘
- **보안 컨텍스트 필요**: Service Worker / 설치는 HTTPS 또는 `localhost`에서만 동작 (예: GitHub Pages)

---

## 디자인 시스템 (Modernist Front)

테마파크의 활기를 **세련된 모더니스트 디렉터리**로 재해석한 디자인. 여백·고대비 타이포그래피·단일 강조색 중심.

### 색상
| 토큰 | 값 | 용도 |
|------|-----|------|
| background | `#f9f9fb` | 페이지 배경 |
| surface-card | `#ffffff` | 카드·버튼 표면 |
| on-surface | `#1a1c1d` | 헤드라인·본문 |
| on-surface-variant | `#434656` | 보조 본문 |
| text-muted | `#6e6e73` | 메타·캡션 |
| border-subtle | `#e5e5e7` | 1px 테두리 |
| primary | `#003ec7` | 링크·지도 버튼 |
| primary-container | `#0052ff` | 주요 액션 버튼 |
| accent-warm | `#ff5c00` | "인기" 배지 |
| tertiary | `#bf3003` | "든든/식사" 배지 |
| error | `#ba1a1a` | "영업 종료" 상태 |

### 타이포그래피
- 글꼴: **Inter** (Google Fonts, 시스템 폰트 폴백)
- display: 48px / 모바일 32px, 800, letter-spacing −0.02em
- headline-md 24px / headline-sm 20px, 700
- body 18/16px, 400 · label 14px 600 · caps 12px 700 · metadata 13px
- 한국어는 `word-break: keep-all`로 단어 단위 줄바꿈

### 형태 · 깊이
- 라운드: 카드 8px / 버튼 4px / 칩·라벨 12px / 배지 2px
- 그림자: 기본 `0 4px 20px rgba(0,0,0,.05)`, 호버 `0 8px 30px rgba(0,0,0,.08)` + 1% lift
- 아이콘: 인라인 SVG 라인 아트 (stroke 1.5)

### 레이아웃
- 컨테이너 최대 1200px, 데스크톱 거터 24px / 모바일 마진 16px, 섹션 간격 80px
- 반응형 카드 그리드: **3열(≥1024px) → 2열(≥768px) → 1열(모바일)**
- 히어로: 데스크톱 2단(7:5) → 모바일 단일 컬럼

---

## 파일 구조

```
.
├── index.html              # 전체 UI + 데이터 + 검색/필터/PWA 로직 (자체 완결형)
├── manifest.webmanifest    # PWA 매니페스트
├── sw.js                   # Service Worker (오프라인 캐시)
├── icon-192.png            # 앱 아이콘
├── icon-512.png
├── icon-maskable-192.png   # maskable 아이콘
├── icon-maskable-512.png
└── README.md
```

> CDN(Tailwind·아이콘 폰트) 의존 없이 자체 CSS + 인라인 SVG로 구현되어 오프라인에서도 동일하게 동작합니다.

---

## 로컬 실행

Service Worker는 `file://`에서 동작하지 않으므로 로컬 HTTP 서버로 띄워야 합니다.

```bash
python -m http.server 8080
# http://localhost:8080/ 접속
```

---

## 작업 이력

| 단계 | 내용 |
|------|------|
| 1. 초기 PWA | 경주월드 먹거리 가이드 PWA 구성 (HTML·매니페스트·SW·아이콘) — 따뜻한 오렌지 톤 |
| 2. 배포 | git 저장소 생성 후 GitHub에 push, GitHub Pages 배포 준비 |
| 3. 모바일 그리드 수정 | 카드 그리드가 모바일에서 1열로 펼쳐지도록 수정 (grid에 무효한 `flex-direction` 제거) |
| 4. 모바일 상단 정돈 | 히어로/티켓 제목 크기 축소, 티켓 이모지 겹침 해결, eyebrow 단어 줄바꿈, 아이콘-통계 간격 확보 |
| 5. 모더니스트 개편 | 참고 디자인(Modernist Front) 적용 — Inter 폰트, 모노크롬+블루 팔레트, 라인 아이콘, 소프트 섀도우로 전면 리디자인 |
| 6. 마무리 수정 | Sign In 버튼 제거, 카피라이트 변경 |

각 단계마다 Service Worker 캐시 버전을 올려(`v1`→`v5`) 기존 방문자도 갱신본을 받도록 처리했습니다.

---

© 2026 Jiun-Jeong. All rights reserved.
