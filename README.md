# 📘 BookTune - 도서 기반 AI 음악 추천 서비스

## 프로젝트 개요

**BookTune**은 독서 중 음악을 즐기는 20~30대 직장인을 위한 웹 서비스입니다.  
도서의 분위기와 내용을 바탕으로 **AI가 어울리는 음악을 추천**하거나,  
**사용자 감정에 맞는 음악을 직접 생성**하여 감성적인 독서 경험을 제공합니다.

> **개발 기간**: 2025년 5월 21일 ~ 2025년 5월 26일  
> **팀원**:  
> 👨‍💻 박유현 (Backend) - 팀장  
> 🎨 강민우 (Frontend)

---

## 🧑‍🎨 페르소나

| 대상 | 성향 | 특징 | 니즈 |
|------|------|------|------|
| 20~30대 직장인 | 문화생활 중 독서를 선호 | 독서 중 음악 감상을 즐김 | 독서 분위기에 맞는 음악 추천을 원함 |

---

## 기능 소개

### ✅ 기본 기능

- 도서 목록 제공
- 장르 필터링
- 도서 검색 (제목/저자)
- 도서 상세 정보 페이지

### 🌟 핵심 기능

- **AI 음악 추천**:  
  OpenAI GPT API를 활용하여 도서에 어울리는 음악 추천 (장르, 분위기 등)

- **사용자 프롬프트 입력**:  
  감정, 날씨, 상황 등 사용자 입력 기반 맞춤형 음악 추천

- **(선택) 음악 생성 기능**:  
  Suno, Mubert 등의 API를 활용한 BGM 자동 생성 *(가능한 경우)*

---

## 🔧 기술 스택

| 분야 | 사용 기술 |
|------|-----------|
| Frontend | Vue.js 또는 React.js |
| Backend | Django REST Framework |
| AI 추천 | OpenAI GPT API |
| 음악 생성 | Suno API / Mubert API *(선택)* |
| 데이터 | JSON 파일 기반 도서 정보 or 공공 API |
| 배포 | GitHub Pages / Vercel / Render 등 |

---

## 🗓 개발 일정

| 날짜 | 작업 내용 |
|------|-----------|
| 5/21 (수) | 기획 정리, 프로젝트 초기 세팅 |
| 5/22 (목) | 도서 목록 / 검색 / 필터 기능 구현 |
| 5/23 (금) | 도서 상세 페이지 개발 |
| 5/24 (토) | AI 음악 추천 기능 개발 (GPT 연동) |
| 5/25 (일) | 사용자 프롬프트 기능 추가, UI 개선 |
| 5/26 (월) | 통합 테스트, 배포, 발표 준비 |

---

## 👥 팀원 및 역할 분담

### 박유현 (Backend)

- Django API 서버 구축
- 도서 모델 및 DB 설계
- OpenAI 연동 및 음악 추천 로직 구현
- (선택) 음악 생성 API 연동

### 강민우 (Frontend)

- 도서 목록 / 상세 페이지 UI 구현
- 검색, 필터 기능 개발
- 사용자 프롬프트 입력 화면 구성
- 추천 결과 시각화 및 스타일링

---

## ✅ 할 일 목록 (요약)

### Backend

- [ ] Django 환경 세팅 및 API 구조 설계
- [ ] 도서 CRUD 및 검색 API 구현
- [ ] OpenAI 연동 및 음악 추천 프롬프트 구성
- [ ] 사용자 커스텀 프롬프트 로직 처리
- [ ] (선택) 음악 생성 기능 연동

### Frontend

- [ ] 전체 UI 구조 설계 및 컴포넌트화
- [ ] 도서 목록/상세/검색 페이지 구현
- [ ] 사용자 프롬프트 입력 및 결과 출력 구성
- [ ] 반응형 디자인 적용 및 배포

---

## 💡 기대 효과

- 감성적 독서 경험 확장 (음악 + 독서의 시너지)
- AI 기반 맞춤형 문화 콘텐츠 추천 경험 제공
- 프롬프트 기반 사용자 참여형 웹서비스 구현

---

## 📄 라이선스

MIT License © 2025 BookTune Team
