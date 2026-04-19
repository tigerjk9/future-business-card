# CLAUDE.md — 미래 명함 메이커

## 한 줄 정의
입력(이름·MBTI·관심사·강점) + 사진(선택) → AI가 만든 2036년 가상 명함 + 자서전 → PNG 다운로드.

## 라이브 / 저장소
- 🌐 https://future-business-card.vercel.app/
- 🐙 https://github.com/tigerjk9/future-business-card

## 기술 스택
- 단일 `index.html` (Vanilla JS)
- Tailwind CSS CDN + Pretendard + html2canvas 1.4.1
- Gemini 2.5 Flash Text (`gemini-2.5-flash`, JSON 모드, temperature 0.95)

## 핵심 데이터 구조
- `MBTI_QUESTIONS[]`: 10문항 (E/I × 3, S/N × 3, T/F × 2, J/P × 2) + 각 선택지의 axis value
- `MBTI_DATA{}`: 16유형 별명 + 한국어 강점 (40~50자)
- 명함 데이터: `{ name, company, title, slogan, email, website, bioTitle, bio, mbti }` (AI JSON 응답)
- `profilePhoto`: dataURL (선택, 4MB 이하)

## 핵심 결정
- **MBTI 10문항 빠른 테스트** (모달, 1분) — 결과 적용 시 MBTI 칩 자동 선택 + 강점 자동 입력 (수정 가능)
- **3D 플립 카드** — 클릭 시 0.9s rotateY(180deg), 앞면=명함 / 뒷면=자서전
- **프로필 사진 업로드** (선택) — 좌측 사이드바 90px 원형 아바타 (사진 또는 이름 첫 글자)
- **Gemini Text JSON 모드** — 회사명/직책/슬로건/이메일/자서전을 한 번에 생성

## 자주 마주치는 이슈
- **이름 글자 fake bold:** `font-weight: 900`이 캡처 시점에 fallback fake bold로 흐릿해짐 → **800 사용** + `document.fonts.load("800 36px Pretendard", "한글샘플")` 트리거 + onclone에서 `#bc-name` 강제 스타일
- **세로 회전 텍스트 잘림:** `transform: rotate(-90deg)` 텍스트가 카드 밖으로 → 가로 배지로 교체 (`.bc-tag`)
- **그라디언트 텍스트 색 섞임:** html2canvas는 `-webkit-background-clip:text` 미지원 → onclone에서 단색 치환
- **뒷면 캡처 시 거울상:** PNG 다운로드 직전 항상 앞면으로 토글 후 캡처

## 변경 핵심 이력
- 2026-04-19: 초기 출시 → MBTI 10문항 + 강점 자동 입력 → 3D 플립 카드 → 프로필 사진 업로드 + 사이드바 확장 → 이름 fake bold 수정

## 관련 문서
- [PRD.md](./PRD.md)
