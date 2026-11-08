# 머스닥 (MUKSDAQ)
소비자 수요 ↔ 점주 혜택 제안 외식 플랫폼. HTML/CSS/JS만 사용(빌드 없음) → GitHub Pages로 바로 배포 가능.

## 폴더 구조 (파일 단위로 담당자 분배)
```
index.html            로그인 + 소비자/점주 선택
home.html             공통 홈 (역할별 시작 화면 안내)
profile.html          공통 내 프로필 / 로그아웃
assets/style.css      공통 디자인 (색상 변수 :root 수정)
assets/common.js      로그인 상태·상단바·하단탭·샘플데이터
user/   market · search · saved · stores · store · reserve · demand-index · account · order · history · ratings · favorites · notifications · demand-new · demand-done · offers · offer-detail
owner/  dashboard · offer-new · offer-sent · reservations · report
```
## 화면 흐름
- 소비자: 로그인 → 시장(market) → 수요 등록 → 등록 완료 → 받은 제안 → 제안 상세/예약 → 시장
- 점주: 로그인 → 대시보드 → 제안 등록 → 발송 확인 → 예약/문의 관리 → 분석 리포트
## 작업 규칙
1. 내 화면 HTML 안의 `<main>` 내용만 수정. 2. 공통 색/버튼은 style.css 클래스(.card .btn .chip .tag) 재사용.
3. 새 화면은 기존 파일을 복사해 `MK.init()` 줄을 유지하고, 메뉴 추가는 common.js의 `tabs`에 한 줄.

## 영수증 인증 (assets/receipt.js)
영수증 사진을 올리면 ① 품질검사(해상도·밝기·대비·선명도) → ② 글자 인식(Tesseract.js, 한글+영문) → ③ 가맹점 대조(상호명/전화번호/주소 중 하나 일치 + 결제금액 인식)를 거쳐 성공/실패를 판정합니다.
- 글자 인식 엔진은 처음 사용할 때 인터넷(cdnjs)에서 불러옵니다.
- 기준값은 `assets/receipt.js` 맨 위 `TH`, 서버 연동 시에는 `ocr()` 함수만 교체하면 됩니다.

## 네이버 지도 (가까운 혜택 매장)
`assets/config.js` 의 `NAVER_KEY` 에 네이버 클라우드 플랫폼의 Maps(Web Dynamic Map) 클라이언트 ID를 넣으면 `user/near-stores.html` 이 네이버 지도로 바뀝니다.
- 발급: https://console.ncloud.com → AI·NAVER API → Application 등록 → Maps(Web Dynamic Map) 선택 → Web 서비스 URL 등록(예: http://127.0.0.1:5500)
- 키가 없거나 인증에 실패하면 기본 지도 이미지로 자동 전환됩니다.

## 카드 등록 테스트용 샘플 (user/card-register.html)
실제 카드사 연동이 아니라 화면용 샘플 카드와 비교합니다. 본인인증 이름은 회원가입 또는 계정관리에서 저장한 이름과 '카드 소유자명'이 같아야 합니다.

| 카드번호 | CVC | 비밀번호 앞 2자리 | 카드사 |
|---|---|---|---|
| 1234 5678 9012 3456 | 123 | 12 | 신한카드 |
| 4111 1111 1111 1111 | 456 | 34 | 국민카드 |
| 5555 4444 3333 2222 | 789 | 56 | 삼성카드 |
| 9411 2233 4455 6677 | 321 | 90 | 하나카드 |
