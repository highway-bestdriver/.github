# BuildX – No-Code AI 모델 생성 플랫폼

## 프로젝트 개요
BuildX는 인공지능(AI) 이론을 학습했지만 코딩에 익숙하지 않은 비전공자 또는 초보자를 위해 설계된 **블록 UI 기반 CNN 모델 제작 플랫폼**입니다. 사용자는 블록 형태의 UI를 통해 CNN 모델을 구성하고, 이를 기반으로 자동 생성된 PyTorch 코드를 통해 GPU 환경에서 학습, 분석 및 피드백까지 받을 수 있습니다.

- **타겟 사용자**: AI 이론은 이해했으나 실습 경험이 부족한 AI 초보자
- **제한 모델 유형**: 이미지 분류 CNN
- **핵심 기능**: 모델 설계, 코드 생성, 학습 실행, 실시간 피드백 및 오류 분석

## 레포지토리 구조
```
highway-bestdriver/
├── BuildX-FE/           # 프론트엔드 (React, Blockly)
├── BuildX-BE/           # 백엔드 (FastAPI, Celery, Redis)
├── Docs/
└── .github            # 메인 실행 및 구조 설명 (본 파일)
```

## 주요 기술 스택
- **Frontend**: React, Recharts
- **Backend**: FastAPI, Celery, Redis, PyTorch, OpenAI GPT API
- **Infra**: Docker, EC2 (Ubuntu), Nginx, WebSocket

## ⚙️ 설치 및 실행 방법
## How to Run
### Front-end
```bash
git clone https://github.com/highway-bestdriver/BuildX-FE.git
cd BuildX-FE
npm install
npm run dev
```
- https://buildx-one.vercel.app/ 에서 실행됩니다.

### Back-end
- 주요 파일:
  `Dockerfile`, `docker-compose.yml`, `requirements.txt`, `app/`, `nginx/conf/`

- **프레임워크**: FastAPI + Celery + Redis + Nginx

- **실행 여부**:  
  `docker-compose.yml`과 `Dockerfile`이 존재하므로 **도커 기반으로 실행 가능**

Docker 및 Docker Compose가 설치되어 있어야 합니다.
```bash
git clone https://github.com/highway-bestdriver/BuildX-BE.git
cd BuildX-BE
docker-compose up --build
```
- FastAPI 서버는 포트 8000에서 실행됩니다.
- WebSocket은 :8000/ws/log로 접속됩니다.
- Celery 작업 큐는 Redis를 브로커로 사용합니다.

### 3. 전체 실행 (Docker 통합 시)
```bash
docker-compose up --build
```

## 테스트 시나리오
- 블록 UI로 CNN 모델 설계 → 완료 후 코드 생성 버튼 클릭
- 생성된 코드 확인 → 학습
- 실시간 학습 로그 및 결과 시각화 확인
   - epoch 마다 그래프를 통해 실시간으로 결과 확인 가능
- 학습 실패 시 GPT 기반 오류 피드백 수신
- 학습 성공 시 최종 분석 및 피드백

## 핵심 기능 요약
| 기능 | 설명 |
|------|------|
| 블록 기반 모델 설계 | Conv2D, MaxPool, Flatten, Dense 등 레이어 블록 지원 |
| GPT 기반 코드 생성 | 정형화된 JSON 구조 → PyTorch 코드로 자동 변환 + 코드 검증 후 반환 |
| 모델 학습 및 실행 | 학습 요청 시 Celery로 비동기 처리 후 GPU 학습 실행 |
| 실시간 로그 전달 | WebSocket 기반으로 학습 로그 실시간 스트리밍 |
| 오류 분석 및 수정 | GPT API를 통해 오류 원인 설명 및 코드 수정 제안 |
| 성능 개선 피드백 | 학습 결과를 바탕으로 구조 수정 제안 제공 |

## 데이터베이스
- 학습 로그 및 결과는 서버 메모리에 임시 저장 (Redis 기반)
- AWS RDS

## 사용한 오픈소스 및 라이브러리
- `PyTorch`, `FastAPI`, `Celery`, `Redis`, `WebSocket`, `OpenAI GPT API`
- `React`, `Recharts`

## 기타 사항
- 오류 분석 및 성능 개선 기능은 모두 GPT-4 API를 활용
- 모델 학습은 PyTorch를 통해 서버에서 직접 실행되며, GPU 환경 기준으로 동작
- 학습 스크립트는 자동 생성된 PyTorch 코드 기준

---
