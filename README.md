# 동해 여름 여행 · 2박 3일 (2026.07.05 ~ 07)

강원 동해·갈남·장호 여행 일정을 한 페이지에서 볼 수 있는 정적 PWA(Progressive Web App)입니다.
Leaflet 지도, 일자별 일정표, 날씨별 대안 플랜, 교통·숙소 정보를 한 화면에서 확인할 수 있습니다.

- **저장소**: https://github.com/Anakin787/gjworld-pwa

---

## 기능 스펙

### 여행 지도 (Leaflet)
- 장소(숙소·관광지) / 맛집 후보 / 우천 대안을 각각 다른 핀 스타일로 표시
- **DAY 필터**: 전체 / DAY 1 / DAY 2 / DAY 3 칩으로 지도에 표시할 장소 전환
- **맛집·우천 대안 토글**: 지도 위 표시 항목을 켜고 끌 수 있음
- 선택한 DAY의 동선을 점선 폴리라인으로 연결
- 핀 클릭 시 사진·시간·메모와 함께 네이버지도 검색 링크 팝업 노출
- 일정표의 장소를 클릭하면 해당 DAY로 전환되며 지도가 그 위치로 이동

### 일정표
- DAY 1(도착) · DAY 2(메인) · DAY 3(마무리) 3개 카드로 구성된 타임라인
- 각 스텝에서 장소 클릭 시 지도 연동, 식사는 후보 맛집 링크로 표시
- `( )`로 표시된 항목은 날씨·컨디션에 따라 생략 가능한 옵션 일정

### 날씨별 플랜 (DAY 2)
- **PLAN A(맑음) / B(비 조금) / C(비 많이)** 3단 대안 제공
- 비 예보 시 우선순위와 대체 장소(환선굴, 논골담길 등)를 함께 안내

### 교통 · 인원 · 숙소
- KTX-이음 가는 길/오는 길 시간표 및 요금
- 테슬라·KTX 탑승 인원 그룹 표시
- 숙소(동해황토민박펜션) 카드에서 네이버지도 바로 연결

### 카카오톡 인앱 브라우저 대응
- 카카오톡 등에서 `target="_blank"` 새 창이 막힐 경우 상단 안내 바 노출, 기본 브라우저로 열기 지원

### PWA
- **오프라인 지원**: Service Worker(`sw.js`)가 앱 셸(HTML·매니페스트·아이콘·지도 라이브러리)을 캐시 우선(cache-first) + 백그라운드 갱신 방식으로 제공
- **매니페스트**: standalone 디스플레이, 192/512 아이콘 + maskable 아이콘
- **보안 컨텍스트 필요**: Service Worker는 HTTPS 또는 `localhost`에서만 동작

---

## 파일 구조

```
.
├── index.html      # 전체 UI + 일정 데이터 + 지도/필터/PWA 로직 (자체 완결형)
├── manifest.json   # PWA 매니페스트
├── sw.js           # Service Worker (오프라인 캐시, 캐시명 donghae-v1)
├── icon-180.png    # Apple touch icon
├── icon-192.png    # 앱 아이콘
├── icon-512.png
├── icon-maskable-512.png
└── README.md
```

---

## 로컬 실행

Service Worker는 `file://`에서 동작하지 않으므로 로컬 HTTP 서버로 띄워야 합니다.

```bash
python -m http.server 8080
# http://localhost:8080/ 접속
```

---

© 2026 Jiun-Jeong. All rights reserved.
