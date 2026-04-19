# 💼 미래 명함 메이커 (Future Business Card)

> **10년 후 나의 명함을 한 장으로 — AI가 가상 회사·직책·슬로건·미래 자서전까지 작성**
> 사진 업로드 없이 텍스트 입력만으로 "2036년의 나"를 명함과 자서전으로 시각화합니다.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Try%20Now-black?logo=vercel)](https://future-business-card.vercel.app/)
[![Gemini](https://img.shields.io/badge/Gemini-2.5%20Flash-blue)](https://ai.google.dev/gemini-api/docs)
[![BYOK](https://img.shields.io/badge/Bring%20Your%20Own-API%20Key-orange)](https://aistudio.google.com/apikey)
[![PNG Export](https://img.shields.io/badge/Export-PNG%20Card-emerald)](#)

---

## 💡 기획 의도

> "10년 후 너의 명함을 미리 받아본다면?"

학생에게 단순히 "꿈이 뭐야?"라고 묻는 대신, **AI가 만든 가상의 명함**을 손에 쥐어주면 진로에 대한 상상이 구체화됩니다. 본 앱은:

- 이름·신분·MBTI·관심사·강점만 입력하면
- Gemini Text가 **2036년 가상 회사·직책·슬로건·이메일·미래 자서전**을 한 번에 작성
- 양면 디자인 명함 + 자서전 한 페이지로 시각화
- PNG로 저장 → 학생에게 기념품으로 배부

3개 진로 시리즈 중 가장 **짧고 강렬한 기념품 형식**입니다.

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| 📝 **간단한 입력 폼** | 이름·신분·MBTI·관심사·강점 5가지만 |
| 🪪 **AI 명함 자동 생성** | 가상 회사명·직책·슬로건·이메일·웹사이트 |
| 📖 **미래 자서전 한 페이지** | "2036년 ___의 하루" 1인칭 묘사 200~350자 |
| 🎨 **글래스모피즘 명함 디자인** | 그라디언트 + 블러 효과로 미래적 분위기 |
| 💾 **PNG 다운로드** | html2canvas로 고해상도 캡처 |
| 🔐 **BYOK 방식** | 사용자 본인의 Gemini API 키, 외부 저장 없음 |

---

## 🚀 바로 사용하기

👉 **[https://future-business-card.vercel.app/](https://future-business-card.vercel.app/)**

### 사용 단계

1. **이름** 입력 (필수)
2. **현재 신분** 선택 (중학생/고등학생/대학생/직장인/기타)
3. **MBTI** 선택 (선택, 16종 + "없음")
4. **관심 분야** 1개 이상 선택 (AI/예술/과학/교육/의료/창업/환경/우주/스포츠/콘텐츠 + 직접 입력 가능)
5. **나의 강점** 한 줄 입력
6. **API 키** 입력 ([Google AI Studio](https://aistudio.google.com/apikey)에서 무료 발급)
7. **「✨ 10년 후 명함 만들기」** 클릭 → 5~15초 대기
8. **「📷 명함 PNG 저장」** → 인쇄해 가져가기!

---

## 🪪 명함 출력 형식

생성되는 양면 디자인:

```
┌──────────────────────────────────────┐
│ — VISIONARY DESIGN LAB —      © 2036 │
│ AI 윤리 디자이너                       │
│                                      │
│        김미래                         │
│   "사람을 향한 기술을 디자인합니다"    │
│                                      │
│ kimirae@future.io  FUTURE BUSINESS  │
│ kimirae.lab        CARD       INFP  │
└──────────────────────────────────────┘

📖 2036년 김미래의 어느 날
"오전 9시, 서울 성수동의 작은 디자인 랩에 들어선다.
 오늘은 새 자율주행 시스템의 UI 윤리 가이드를 검토하는 날.
 동료 박지훈과 커피를 마시며 ..."
```

---

## 🛠️ 기술 스택

| 분류 | 기술 |
|------|------|
| **AI 모델** | Google **Gemini 2.5 Flash** (`gemini-2.5-flash`, JSON 응답 강제) |
| **명함 캡처** | [html2canvas](https://html2canvas.hertzen.com/) 1.4.1 (동적 로드) |
| **프론트엔드** | Vanilla JavaScript (단일 `index.html` 파일) |
| **스타일링** | Tailwind CSS (CDN) + 글래스/오로라 디자인 |
| **타이포그래피** | Pretendard |
| **호스팅** | Vercel (정적, GitHub 연동 자동 배포) |

> 💡 백엔드 서버 없음 · 빌드 도구 없음 · `index.html` 단일 파일

---

## 💡 핵심: 구조화된 JSON 응답

Gemini Text의 `responseMimeType: "application/json"` 옵션으로 다음 스키마를 강제합니다:

```json
{
  "company": "string (12자 이내, 트렌디 회사명)",
  "title": "string (25자 이내, 미래형 직책)",
  "slogan": "string (30자 이내, 모토 한 문장)",
  "email": "string (영문 + future.io 도메인)",
  "website": "string (영문 도메인)",
  "bioTitle": "string (자서전 제목, 25자 이내)",
  "bio": "string (200~350자, 1인칭 시점, 구체적 장소·도구·동료 포함)",
  "mbti": "string",
  "name": "string"
}
```

`temperature: 0.95`로 매번 새로운 결과가 나오도록 설정했습니다.

---

## 📦 로컬 실행

```bash
git clone https://github.com/tigerjk9/future-business-card.git
cd future-business-card
python -m http.server 8000
# 브라우저에서 http://localhost:8000 접속
```

---

## 🔑 API 키 발급 가이드

1. [Google AI Studio](https://aistudio.google.com/apikey) 접속
2. Google 계정 로그인
3. **"Create API Key"** 클릭 → 키 복사
4. 본 앱 입력란에 붙여넣기

> 🔒 **보안:** API 키는 사용자 브라우저 내에서만 사용되며, 외부 서버로 전송·저장되지 않습니다.

---

## 📁 저장소 구성

```
future-business-card/
├── README.md       # 본 문서
├── index.html      # 단일 파일 웹앱 (입력 폼 + 명함 + 자서전)
└── .gitignore
```

---

## 🎯 활용 사례

- 🎓 **학교 진로 부스** - 5분 만에 받는 미래 명함
- 🏫 **진로 캠프** - 캠프 종료 시 기념품 제작
- 📸 **진로 박람회** - 짧은 시간에 깊은 인상
- 🧑‍🏫 **자유학기제** - 진로 상상력 키우기 활동

---

## 🐛 알려진 제약

- Gemini Text 응답 시간: 5~15초
- API 무료 할당량 초과 시 오류 (BYOK 방식이라 사용자별 별도)
- html2canvas는 일부 CSS 효과(특히 backdrop-filter)를 정확히 캡처하지 못할 수 있음 — 명함 디자인은 캡처 호환을 고려해 단순화

---

## 📝 변경 이력

| 날짜 | 내용 |
|------|------|
| 2026-04-19 | 🔄 **3D 플립 카드** 추가 — 명함 클릭 시 0.9s easing으로 Y축 회전 (앞면 명함 ↔ 뒷면 자서전 다이어리 카드) |
| 2026-04-19 | 🧭 **MBTI 10문항 빠른 테스트** 모달 추가 — 1분 검사 후 MBTI 자동 선택 + 16유형별 강점 자동 입력 (수정 가능) |
| 2026-04-19 | 🎨 **명함 디자인 전면 강화** — 좌측 컬러 사이드바 + 도트 패턴 + 이니셜 원형 로고 + 점선 스탬프 + 코너 장식 |
| 2026-04-19 | 🐛 **PNG 색상 버그 수정** — html2canvas의 `-webkit-background-clip:text` 미지원으로 이름이 색깔 섞여 출력되던 이슈 해결 (onclone에서 단색 치환) · 캡처 스케일 2 → 3 (인쇄 품질 ↑) |
| 2026-04-19 | 초기 출시 (Gemini Text JSON 응답 + 양면 명함 + 자서전) |

---

## 🌟 향후 개선 아이디어

- [ ] 사진 업로드 → Gemini Image로 명함 프로필 사진 생성
- [ ] 명함 디자인 테마 선택 (모던/클래식/팝)
- [ ] 양면 명함 PDF 생성 (앞: 명함, 뒤: 자서전)
- [ ] QR 코드(자서전 전체 텍스트 링크) 자동 삽입
- [ ] 다국어 지원 (영어/일본어 명함)

---

## 🔗 관련 프로젝트 (진로 시리즈)

| 프로젝트 | 설명 | 라이브 |
|---------|------|--------|
| **Career Photo Studio** | 사진 → 8가지 직업 변신 | [link](https://career-photo-studio.vercel.app/) |
| **RIASEC Career Cards** | 흥미 검사 → 매칭 직업 3장 카드 | [link](https://riasec-career-cards.vercel.app/) |
| **Future Business Card** *(본 프로젝트)* | 10년 후 나의 명함 + 자서전 | [link](https://future-business-card.vercel.app/) |

본 프로젝트는 [AI Hands-On 부스](https://ai-hands-on-booth-v2.vercel.app/)에 등록되어 있습니다.

---

## 🙏 크레딧

- **Google Gemini 2.5 Flash** — 텍스트 생성 (JSON 모드)
- **html2canvas** — 클라이언트 사이드 명함 PNG 캡처
- **Tailwind CSS** · **Pretendard**

---

## 📝 라이선스

MIT License

---

## 👤 제작자

**김진관 (닷커넥터)**
- GitHub: [@tigerjk9](https://github.com/tigerjk9)
- Linktree: [litt.ly/dot_connector](https://litt.ly/dot_connector)

---

> 💼 **지금 바로 [미래 명함 메이커](https://future-business-card.vercel.app/)에서 2036년의 명함을 받아보세요!**
