# 🎯 Video-based VQA Authentication System

## 📌 Overview
영상 기반 VQA(Visual Question Answering)를 활용하여  
매크로 및 자동화 봇을 탐지하고 차단하는 인증 시스템입니다.

기존 CAPTCHA의 한계를 극복하기 위해  
동적 영상과 추론 기반 문제를 활용한 새로운 인증 방식을 설계했습니다.

---

## 🚀 Key Features

- 🎥 OpenCV 기반 마라톤 시뮬레이션 영상 생성
- 🧠 추론 기반 VQA 문제 자동 생성
- 🔊 LLM + TTS 기반 음성 안내 생성
- ⚙️ LangGraph 기반 멀티 에이전트 파이프라인
- 🔁 batch + 병렬 처리 기반 대량 콘텐츠 생성
- ☁️ S3 + DB 기반 콘텐츠 저장 구조
- 🔐 매크로 대응을 위한 보안 설계

---

## 🧩 System Architecture
Supervisor Agent
→ Worker Agent (LangGraph)
→ generate_video → validate_video → generate_questions → generate_script → generate_tts → upload_and_save


## 🛠️ Tech Stack

### Language
- Python

### AI / ML
- OpenAI API (LLM, TTS)
- LangGraph
- Hugging Face Transformers
- PyTorch

### Backend
- FastAPI

### Infra
- AWS S3

### Database
- PostgreSQL
- Redis

---

## 🔥 Key Challenges & Solutions

### 1. 이미지 VQA 한계 → 영상 기반 전환
- 비용 증가 및 보안 취약 문제 발생
- OpenCV 기반 시뮬레이션으로 전환
- 결과 데이터 완전 통제

### 2. 보안 vs 사용자 경험 Trade-off
- 모든 사용자 인증 시 UX 저하
- 의심 사용자만 VQA 적용 (선별적 인증)

### 3. 매크로 공격 대응
- 단일 프레임 캡처로 문제 해결 가능
- 장애물 + 시간 기반 변화 도입
- 이미지 캡처 공격 차단

### 4. 문제 품질 문제
- 일부 문제 난이도 과도
- validation 노드 도입
- 품질 기준 통과 데이터만 사용

---

## 📊 Result

- 영상 + 문제 + 음성 자동 생성 파이프라인 구축
- 대량 콘텐츠 생성 가능 구조
- 매크로 대응 인증 시스템 구현

---

## 💡 Insights

- 단순 생성보다 **검증이 더 중요**
- 멀티 에이전트의 핵심은 **역할 분리**
- 비용은 모델이 아니라 **재생성에서 발생**
- 완벽한 탐지보다 **공정성 중심 설계가 중요**

---
