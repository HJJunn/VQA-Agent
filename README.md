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
<img width="2304" height="266" alt="image" src="https://github.com/user-attachments/assets/36b2a773-a080-4fcc-ad37-8db401587a08" />

본 시스템은 다음과 같은 선형 및 조건부 로직을 포함하는 상태 머신 구조를 가집니다.

### 1.Generate Video
OpenCV를 이용한 마라톤 시나리오 렌더링.

### 2.Validate Video
생성된 영상 데이터의 유효성 및 중복 여부 체크.

### 3.Generate Questions
영상 메타데이터 기반의 VQA 질문 세트 생성 

### 4.Generate Script
영상 상황에 맞는 해설용 방송 스크립트 생성 (LLM).

### 5.Generate TTS
스크립트를 음성 파일(.mp3)로 변환 (OpenAI TTS).

### 6.Upload & Save
결과물을 AWS S3 및 데이터베이스에 영구 저장.


## 🛠️ Tech Stack

### Language
- Python

### AI / ML
- OpenAI GPT-5.4-mini
- OpenAI TTS
- LangGraph
- LangChain
- PyTorch

### Backend
- FastAPI

### Infra
- Docker, Kubernetes (EKS)
- AWS S3
- AWS ECR

### Database
- MongoDB

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

## 🚀 Getting Started

### Prerequisites
- Docker & Docker Desktop
- AWS CLI (ECR access)
- OpenAI API Key

### Installation
```
# 레포지토리 클론
git clone https://github.com/your-username/VQA_AGENT.git
cd VQA_AGENT

# 가상환경 구축
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Build & Deploy
```
# Docker 빌드 (linux/amd64 플랫폼 기준)
docker build --platform linux/amd64 -t [YOUR_ECR_URL]/on-race-vqa:latest .

# ECR 푸시
aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin [YOUR_ACCOUNT_ID].dkr.ecr.ap-northeast-2.amazonaws.com
docker push [YOUR_ACCOUNT_ID].dkr.ecr.ap-northeast-2.amazonaws.com/on-race-vqa:latest

# K8s 재배포
kubectl rollout restart deployment on-race-vqa -n t6-on-race-prod
```
---
## UX
<img width="700" height="800" alt="image" src="https://github.com/user-attachments/assets/eb53883c-e757-4443-8cd0-d7c587bc5573" />


