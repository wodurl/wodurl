# 양재혁 · DevOps / Cloud Engineer
 
**운영 중인 시스템에서 원인을 끝까지 파고, 재발하지 않게 구조로 고치는 엔지니어**
 
AWS · Terraform · Kubernetes · GitOps · CI/CD
 
[Portfolio(Notion)](https://app.notion.com/p/2f1d9077c730800cb72ce0cbf1e16b06?source=copy_link) · [Email](mailto:z94648569@gmail.com)

---
 
## 🏆 Featured Projects
 
### 뭉치(MoongCheap) — AI 역경매 공동구매 플랫폼 인프라
**KT Cloud TECH UP 2기 통합 프로젝트 대상** · 2026.08–10 · 인프라 파트장(5인)
[`V-MoongCheap/MoongCheap-Cloud`](https://github.com/V-MoongCheap/MoongCheap-Cloud)
 
- AWS(서비스·데이터) + KT Cloud(관리 서버·2차 백업) 멀티 클라우드 아키텍처 설계
- 비작업 시간 Open/Close 자동화 단독 구현 — Git PR로 스케줄 관리, flock·멱등 재조정·PDB 교착 시 강제 종료
- RDS → KT Object Storage 백업 파이프라인 — GPG 암호화, 객체 잠금 14일, sha256 검증
- 한 번도 끝까지 돈 적 없던 Jenkins CI 복구 → **기동 96분 → 2.6분, 빌드 45분 → 16분**
- system 노드 메모리 쏠림 해소 **request 98% → 75%**, backend 2 replicas + PDB
- Cloud 레포 커밋 **208건, 팀 내 최다**
### HailCast — 예측형 오토스케일링 & FinOps
kt cloud TECH UP 실무 프로젝트 · 2026.07–08 · 앱팀 백엔드·CI/CD
[`ThisPod-ThatPod/project3-hailcast-app`](https://github.com/ThisPod-ThatPod/project3-hailcast-app)
 
- GitHub Actions → ECR → manifests → ArgoCD 이미지 태그 자동 갱신 (봇 커밋 36건)
- 봇 PR이 팀원 수정을 되돌리는 경합 문제 → 직접 push + rebase 재시도로 재설계
- 개인 PAT → GitHub App 설치 토큰 이관, OIDC로 장기 키 없는 ECR push
- FastAPI 백엔드 5개 서비스 MVP, SQS → Worker → 예측 → KEDA 스케일링 E2E 검증
> ℹ️ 이 레포의 `yjh-*` 브랜치 커밋은 팀 공용 설정으로 다른 계정에 귀속되어 있습니다.
 
### TicketGuard — 티켓팅 서비스 DB HA · IaC
KT Cloud TECH UP 심화 프로젝트 · 2026.06 · DB 계층·IaC 담당
[`ohyoungsik/ICT-Studio-INFRA`](https://github.com/ohyoungsik/ICT-Studio-INFRA)
 
- PostgreSQL 16 HA (Primary 1 + Replica 2, repmgr 자동 failover, HAProxy 쓰기 엔드포인트)
- Primary 강제 종료 → 자동 승격 → 전환까지 14단계 장애 테스트
- 평면 Terraform을 10개 모듈로 분리, **moved 블록 119개로 재생성 없이 state 보존**
- Terraform → Ansible(동적 inventory) → GitHub Actions 배포 자동화
---
 
## 🛠 Tech Stack
 
**Cloud** &nbsp; ![AWS](https://img.shields.io/badge/AWS-232F3E?logo=amazonwebservices&logoColor=white) ![KT Cloud](https://img.shields.io/badge/KT_Cloud-E60012?logoColor=white) ![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?logo=cloudflare&logoColor=white)
 
**IaC / Config** &nbsp; ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?logo=terraform&logoColor=white) ![Ansible](https://img.shields.io/badge/Ansible-EE0000?logo=ansible&logoColor=white)
 
**Container / Orchestration** &nbsp; ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) ![Helm](https://img.shields.io/badge/Helm-0F1689?logo=helm&logoColor=white) ![Karpenter](https://img.shields.io/badge/Karpenter-FF9900?logoColor=white) ![KEDA](https://img.shields.io/badge/KEDA-0066CC?logoColor=white)
 
**CI/CD · GitOps** &nbsp; ![Jenkins](https://img.shields.io/badge/Jenkins-D24939?logo=jenkins&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white) ![Argo CD](https://img.shields.io/badge/Argo_CD-EF7B4D?logo=argo&logoColor=white)
 
**Observability** &nbsp; ![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)
 
**Data / Backend** &nbsp; ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
 
---
 
## 🔍 Troubleshooting Highlights
 
| 문제 | 원인 | 해결 |
| --- | --- | --- |
| 태그 한 줄 변경 plan이 12 destroy | 모듈 `depends_on` → data source 지연 → `principal_arn` unknown → ForceNew | 암묵 의존으로 대체 → 0 destroy |
| OAuth redirect가 `http://`로 생성 | Envoy가 `X-Forwarded-Proto`를 덮어씀 (경로별 직접 호출로 특정) | `numTrustedHops: 1` |
| Pod 예고 없는 재시작 | "CI 실패" 가설 반박 → 실제는 Karpenter 노드 정리 | do-not-disrupt → 2 replicas + PDB |
| 재배포 후 Replica가 독립 DB로 동작 | bind mount 잔존 데이터로 클론 생략 | 배포 · 초기화 · failback 스크립트 분리 |
 
---
 
## 📜 Education & Experience
 
- **KT Cloud TECH UP 2기** 수료 (2026.10)
- **Bosch** 현장실습
