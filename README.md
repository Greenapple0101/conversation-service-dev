## 🚀 Conversation Service (MLOps 기반 자동 배포 시스템)

CI/CD + Kubernetes 기반으로  
코드 품질 검증 → 자동 PR → 자동 배포까지 연결된  
운영형 AI 서비스 배포 파이프라인 프로젝트
<img width="2816" height="1376" alt="image 105" src="https://github.com/user-attachments/assets/c711e400-9374-407f-8899-8ab85f2ab8b3" />

이 문서는 Conversation Service의 배포 방법을 설명합니다. 
## 배포 환경

- **컨테이너 런타임**: Docker
- **오케스트레이션**: Kubernetes (k3s)
- **CI/CD**: Jenkins
- **포트**: 7003 (Gunicorn), 8100 (Kubernetes Service)

## 🎯 프로젝트 목적

기존 배포 방식은 다음 문제가 있음:

- 코드 품질 검증 없이 배포됨
- 성능 저하 버전이 그대로 운영 반영됨
- 수동 배포로 인해 실수 발생 가능

→ 이를 해결하기 위해

- SonarCloud 기반 품질 게이트
- 자동 PR 생성
- Kubernetes 자동 배포

까지 연결된 CI/CD 파이프라인을 구축

## CI/CD 파이프라인 (Jenkins)
<img width="2950" height="1440" alt="Gemini_Generated_Image_ynjbbeynjbbeynjb" src="https://github.com/user-attachments/assets/d53c8547-453a-4215-add9-8edbae5f975d" />

## 🔄 CI/CD 파이프라인

코드 변경이 발생하면 자동으로 다음 과정이 실행됩니다:

1. GitHub Webhook → Jenkins 트리거
2. Pytest → 기능 검증
3. SonarCloud → 코드 품질 분석
4. Quality Gate → 기준 미달 시 배포 중단
5. Docker Image 빌드 및 푸시
6. Kubernetes(k3s) 자동 배포

→ 품질이 보장된 코드만 운영 환경에 반영됩니다

### 브랜치별 동작

- **develop 브랜치**:
  - SonarCloud 분석
  - Docker 이미지 빌드 및 푸시
  - main 브랜치로 PR 자동 생성

- **main 브랜치**:
  - SonarCloud 분석
  - Docker 이미지 빌드 및 푸시
  - k3s 클러스터에 자동 배포

## 🧱 아키텍처 개요

- GitHub → 코드 push
- Jenkins → CI/CD 실행
- SonarCloud → 코드 품질 분석
- Docker → 이미지 빌드
- Kubernetes(k3s) → 서비스 배포
- Prometheus/Grafana → 모니터링

## 📈 결과

- 품질 기준 미달 코드 자동 차단
- 수동 배포 제거 → 실수 감소
- 배포 시간 단축 및 안정성 향상

→ 단순 배포가 아닌 “운영형 DevOps 시스템” 구축
