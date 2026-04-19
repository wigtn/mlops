# DevOps 엔지니어 심층 이해 레포

> 목적: "DevOps 엔지니어가 도대체 뭐하는 사람인가"를 스스로 설명할 수 있을 때까지 정리.
> MLOps 포지션으로 가는 디딤돌이기도 하므로, DevOps를 이해 못하면 MLOps는 해석 불가.

---

## 1. DevOps란 무엇인가 — 먼저 역사적 맥락

### 1-1. 왜 생겼나
예전에는 **Dev(개발팀)** 와 **Ops(운영팀)** 이 분리되어 있었다.
- Dev: "일단 기능 빨리 만들어서 던지자"
- Ops: "서버 터질 것 같으니 배포하지 마라"
→ 서로 목표가 반대. 배포가 느려지고 장애가 잦아짐.

**DevOps = 이 둘의 벽을 허물고, "빠르게 + 안정적으로" 를 동시에 달성하자는 문화/철학.**

### 1-2. 핵심 아이디어
- **자동화**: 사람이 손으로 하면 실수 → 스크립트/파이프라인으로 돌린다
- **Infrastructure as Code (IaC)**: 서버 설정도 코드로 관리 (버전 관리, 리뷰, 재현 가능)
- **Continuous Integration / Continuous Deployment (CI/CD)**: 코드 커밋 → 자동 테스트 → 자동 배포
- **관측 가능성 (Observability)**: 로그/메트릭/트레이싱으로 시스템 상태를 항상 파악
- **피드백 루프**: 장애가 나면 빨리 알고, 빨리 고치고, 재발 방지

### 1-3. 중요한 오해
**"DevOps 엔지니어"라는 직무 자체가 논쟁적이다.** DevOps는 원래 **문화**였는데, 회사들이 "그걸 전담하는 사람"을 뽑기 시작하면서 직무화됨. 그래서 실제로는:

| 직함 | 실제 하는 일 |
|---|---|
| DevOps Engineer | CI/CD, 클라우드 인프라, 자동화 — **"개발팀이 편하게 배포하게 해주는 사람"** |
| SRE (Site Reliability Engineer) | 위의 일 + **신뢰성/가용성 전담** (SLA, SLO, Error Budget) |
| Platform Engineer | 위의 일 + **개발자 전용 내부 플랫폼 구축** (Internal Developer Platform, IDP) |
| Cloud Engineer | AWS/GCP 인프라 설계/운영 위주 |
| Infrastructure Engineer | 네트워크/서버 물리 레이어 위주 |

**회사마다 정의가 제각각이다.** 공고 볼 때 반드시 업무 내용을 읽고 판단해야 함.

---

## 2. DevOps 엔지니어의 실제 업무 (하루 단위)

### 2-1. 전형적인 하루 (중급 DevOps)
```
09:30  Slack 확인, 야간 알람 리뷰 (Datadog/PagerDuty)
10:00  스탠드업 — "어제 뭐했는지, 오늘 뭐할지, 블로커"
10:30  CI 파이프라인 깨진 거 디버깅 (왜 GitHub Actions 빌드가 5분 → 20분 늘었나)
12:00  점심
13:00  Terraform PR 리뷰 — 개발팀이 새 RDS 인스턴스 요청
14:00  K8s 클러스터 노드 수 조정, HPA (Horizontal Pod Autoscaler) 튜닝
15:30  개발자 A의 "내 서비스 배포 왜 실패하냐" 문의 대응
16:30  Prometheus 알림 규칙 추가 (p99 latency > 500ms면 Slack으로 알림)
17:30  다음주 인프라 마이그레이션 계획 문서 작성
18:30  퇴근 (온콜 당번이면 퇴근 후에도 phone 들고 있어야 함)
```

### 2-2. 업무를 유형별로 분류

| 유형 | 비중 | 구체 예시 |
|---|---|---|
| **빌드/배포 자동화** | 25% | GitHub Actions 워크플로 작성, Jenkins job 관리, 배포 스크립트 작성 |
| **인프라 프로비저닝 (IaC)** | 20% | Terraform으로 AWS 리소스 생성/변경, 상태 관리, 리뷰 |
| **컨테이너 오케스트레이션** | 20% | Kubernetes 매니페스트 작성, Helm chart, Ingress/Service 설정 |
| **모니터링/알람** | 15% | Prometheus/Grafana 대시보드, Datadog 알림 규칙, 로그 수집(ELK, Loki) |
| **장애 대응 (Incident)** | 10% | 온콜, Runbook 작성, 포스트모템 |
| **보안/컴플라이언스** | 5% | 시크릿 관리 (Vault/AWS Secrets Manager), IAM 정책 |
| **개발자 지원** | 5% | "어떻게 배포해요" 문의, 사내 문서화 |

---

## 3. 자격 요건 — 기술 스택 체크리스트

### 3-1. 공통 핵심 (일본 공고 기준 출현 빈도)

| 스킬 | 출현 빈도 | 설명 |
|---|---|---|
| **Kubernetes** | 59% | 컨테이너 오케스트레이션의 표준. 필수 |
| **AWS** | 48% | 클라우드 플랫폼. GCP/Azure 중 하나는 필수 |
| **Python** | 48% | 자동화 스크립트의 기본 언어 |
| **Terraform** | 48% | IaC 표준 도구 |
| **CI/CD** | 41% | GitHub Actions, Jenkins, CircleCI, GitLab CI |
| **Linux** | 37% | 모든 서버의 기반. Bash, systemd, cgroups, namespace 이해 |
| **Docker** | 33% | 컨테이너화의 기본 |
| **GCP** | 26% | AWS 대안 |
| **모니터링** | 22% | Prometheus, Grafana, Datadog, Splunk |

### 3-2. 레벨별 요구사항

| 레벨 | 경력 | 요구 수준 | 한국 연봉 | 일본 연봉 |
|---|---|---|---|---|
| Junior | 0~2년 | Docker/Git/Linux 기본, CI 파이프라인 수정 가능 | 3,500~5,000만 | 500~700만엔 |
| Mid | 2~5년 | K8s 프로덕션 운영, Terraform 설계, 온콜 대응 | 5,000~8,000만 | 700~1,100만엔 |
| Senior | 5년+ | 아키텍처 설계, 팀 리딩, 멀티 클러스터/멀티 리전 | 8,000만+ | 1,100~1,600만엔 |
| Staff/Principal | 8년+ | 플랫폼 전략, 조직 전반 인프라 표준 수립 | 1.2억+ | 1,600만엔+ |

### 3-3. "초급 DevOps"라 말할 수 있으려면 (현 상태 진단용)

- [ ] Dockerfile 직접 작성해서 이미지 빌드/푸시 가능
- [ ] Docker Compose로 로컬 멀티 컨테이너 실행 가능
- [ ] Kubernetes에서 Deployment/Service/Ingress 매니페스트 읽고 쓰기 가능
- [ ] GitHub Actions 워크플로 직접 작성 (lint → test → build → deploy)
- [ ] AWS or GCP 한 곳에서 VPC/EC2/RDS/S3/IAM 기본 이해
- [ ] Terraform으로 간단한 리소스 만들어본 경험
- [ ] Linux 기본 명령어 (grep, awk, sed, systemctl, journalctl) 불편 없음
- [ ] Prometheus 메트릭 읽기, Grafana 대시보드 수정 가능
- [ ] nginx/ALB 같은 L7 로드밸런서가 뭐하는지 설명 가능

→ 6개 이상 체크면 "초급 DevOps", 3~5개면 "풀스택 중 DevOps 잡부" 수준.

---

## 4. 각 기술이 "무엇을 의미하는가" — 개념적 이해

### 4-1. Docker (컨테이너)
- **문제**: "내 PC에선 되는데 서버에선 안돼요" → 환경 차이
- **해결**: 앱 + 라이브러리 + OS 설정을 하나의 "이미지"로 묶어서 어디서나 똑같이 실행
- **내부 원리**: Linux의 namespace(프로세스 격리) + cgroups(리소스 제한) + overlay filesystem
- **왜 중요**: 배포 단위 표준화. MLOps도 모델을 Docker로 패키징함

### 4-2. Kubernetes (K8s)
- **문제**: 컨테이너 100개를 어떻게 배포/재시작/스케일링/네트워크 연결하나?
- **해결**: 선언적 설정(YAML)으로 "원하는 상태" 정의 → K8s가 알아서 맞춤
- **핵심 개념**:
  - Pod: 컨테이너 실행 단위
  - Deployment: Pod를 몇 개 띄울지
  - Service: Pod 앞에 고정 IP/DNS
  - Ingress: 외부 트래픽 라우팅
  - ConfigMap/Secret: 설정값/비밀 관리
- **왜 MLOps의 기반**: GPU 스케줄링, 분산 학습/추론 모두 K8s 위에서. vLLM도 K8s Operator 있음

### 4-3. Terraform (IaC)
- **문제**: AWS 콘솔에서 클릭해서 만든 서버는 "어떻게 만들어졌는지" 기록이 없음
- **해결**: 인프라를 코드로 선언 → Git으로 버전관리, 리뷰, 재현
- **핵심 개념**:
  - Provider: AWS/GCP 등
  - Resource: 실제 리소스
  - State: 현재 상태 스냅샷 (중요, 절대 손으로 건들면 안됨)
  - Module: 재사용 단위

### 4-4. CI/CD
- **CI (Continuous Integration)**: 코드 푸시 → 자동으로 빌드/테스트. "내 PR이 뭔가 깨뜨리진 않았는지" 확인
- **CD (Continuous Deployment)**: 테스트 통과하면 자동 배포
- **파이프라인 예시**:
  ```
  PR 생성 → lint → unit test → build Docker image → push to ECR
  → staging 배포 → e2e test → (승인) → production 배포
  ```

### 4-5. 관측 가능성 (Observability) 3요소
- **Metrics**: 숫자 (CPU 80%, 요청 100 req/s) → Prometheus
- **Logs**: 텍스트 이벤트 → Loki, ELK
- **Traces**: 요청이 서비스 간 어떻게 흐르는지 → Jaeger, Datadog APM

### 4-6. SRE의 핵심 개념 (DevOps에서도 쓰임)
- **SLI (Service Level Indicator)**: 측정값 (e.g. 성공 요청 비율)
- **SLO (Service Level Objective)**: 목표 (e.g. 99.9% 성공)
- **SLA (Service Level Agreement)**: 고객과의 계약 (e.g. 99.5% 미달 시 환불)
- **Error Budget**: SLO에서 허용 가능한 실패량. 이 예산 안에서 빠르게 배포해도 OK

---

## 5. DevOps → MLOps 브리지

### 5-1. MLOps가 DevOps에서 추가되는 것
- **모델 버전 관리**: 코드 + 데이터 + 모델 가중치 (MLflow, Weights & Biases)
- **실험 추적**: 어떤 하이퍼파라미터로 어떤 성능이 나왔는지
- **피처 스토어**: 학습/추론에서 같은 피처 사용 보장 (Feast)
- **모델 서빙**: vLLM, SGLang, Triton, TorchServe
- **GPU 관리**: NVIDIA Device Plugin, MIG, GPU Operator
- **파이프라인**: Kubeflow, Airflow, Argo Workflows
- **모델 모니터링**: 데이터 드리프트, 모델 성능 저하 감지

### 5-2. DevOps 경험이 MLOps에 그대로 쓰이는 영역
- K8s 운영 → GPU K8s 운영
- CI/CD → 모델 학습/배포 파이프라인
- Terraform → GPU 클러스터 프로비저닝
- Prometheus → GPU 사용률, 추론 latency 모니터링
- Docker → 모델 컨테이너화

→ **결론**: DevOps 2년 + ML 지식 추가 = MLOps. 지름길이 DevOps 정착.

---

## 6. Phase별 학습 로드맵 (career-plan과 연동)

### Phase 1 (0~6개월) — DevOps 초급 완성

| 주차 | 주제 | 교재/실습 |
|---|---|---|
| 1~2 | Linux + Bash 심화 | [MIT Missing Semester](https://missing.csail.mit.edu/) |
| 3~4 | Docker 완전 이해 | [Docker 공식 Get Started](https://docs.docker.com/get-started/), namespace/cgroups 실습 |
| 5~8 | Kubernetes 기초 | [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) (요약판), kind로 로컬 클러스터 |
| 9~10 | Terraform | [HashiCorp Learn](https://developer.hashicorp.com/terraform/tutorials) |
| 11~12 | CI/CD | GitHub Actions로 포트폴리오 프로젝트 배포 파이프라인 |
| 13~16 | AWS 기초 | [AWS SAA-C03](https://aws.amazon.com/certification/certified-solutions-architect-associate/) 교재 |
| 17~20 | 관측성 | Prometheus/Grafana로 내 앱 메트릭 수집 실습 |
| 21~24 | 종합 포트폴리오 | RAG 챗봇을 K8s + Terraform + GitHub Actions + Prometheus 풀스택으로 |

### Phase 2 (6~24개월) — DevOps 중급

- **CKA (Certified Kubernetes Administrator)** 자격 취득
- **AWS SAA** 또는 **GCP ACE** 자격
- 프로덕션 K8s 클러스터 운영 경험 (입사 후)
- 온콜 참여, 포스트모템 작성 경험
- Helm chart 직접 작성, GitOps (ArgoCD/Flux) 도입

### Phase 3 (24개월~) — MLOps 전환

- Kubeflow 또는 Ray on K8s로 분산 학습
- vLLM/SGLang 프로덕션 배포
- GPU Operator, MIG, Device Plugin 이해
- 모델 서빙 latency 튜닝

---

## 7. 이해도 체크 질문 (스스로 답할 수 있어야 함)

### 입문 레벨
1. 왜 Dev와 Ops를 합친 DevOps가 필요했나?
2. Docker와 VM의 차이는?
3. Kubernetes가 없으면 뭐가 불편한가?
4. IaC가 콘솔 클릭보다 좋은 이유 3가지?
5. CI와 CD의 차이는?

### 중급 레벨
6. K8s의 Pod가 죽으면 누가 새로 만드나? (답: Controller, 구체적으로는 ReplicaSet)
7. Terraform state 파일이 왜 중요한가? 손상되면?
8. Blue-Green 배포와 Canary 배포의 차이?
9. SLO가 99.9%일 때 월간 허용 다운타임은? (약 43분)
10. 온콜 중 새벽 3시에 알람이 왔다. 첫 3분 동안 뭘 해야 하나?

### MLOps 연결 레벨
11. GPU 노드를 K8s에서 어떻게 스케줄링하나? (답: NVIDIA Device Plugin + nodeSelector/tolerations)
12. 모델 A/B 테스트를 K8s로 구현한다면 어떻게?
13. PagedAttention이 K8s 클러스터 운영에 주는 영향은? (KV 캐시 메모리 예측 가능 → 리소스 요청 명확)
14. 학습 Job과 추론 Service의 K8s 리소스 관리 차이는?

---

## 8. 일본에서 DevOps로 지원 가능한 회사 (career-plan Phase 2와 연동)

| 회사 | 포지션 예시 | Link |
|---|---|---|
| **Mercari** | SRE / Platform Engineer | https://careers.mercari.com/en/ |
| **Rakuten** | DevOps / SRE / Cloud Engineer | https://japan-job-en.rakuten.careers/ |
| **LY Corporation** | SRE | https://www.lycorp.co.jp/en/ |
| **Shippio** | DevOps Engineer | https://www.tokyodev.com/companies/shippio/jobs/devops-engineer |
| **Beacon Platform** | Junior DevOps | https://www.tokyodev.com/companies/beacon-platform/jobs/junior-devops-engineer |
| **Mujin** | DevOps Engineer | https://relocate.me/japan/tokyo/mujin/devops-engineer-8784 |
| **CTW** | DevOps Engineer | https://startup.jobs/devops-engineer-ctw-4154000 |

**Junior DevOps 포지션을 명시한 회사(Beacon Platform 등)가 진입점으로 특히 유리.**

---

## 9. 참고 자료 북마크

### 필독
- [The DevOps Handbook](https://itrevolution.com/product/the-devops-handbook-second-edition/) — 바이블
- [Google SRE Book](https://sre.google/books/) — 무료, SRE 원조
- [roadmap.sh/devops](https://roadmap.sh/devops) — 학습 경로 시각화

### 일상 참고
- [Kubernetes 공식 문서](https://kubernetes.io/docs/)
- [Terraform Registry](https://registry.terraform.io/)
- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/)

### 일본어 자료 (발신용)
- Qiita: DevOps 태그
- Zenn: SRE, Kubernetes 토픽

---

## 10. 핵심 메시지 요약

1. **DevOps는 직무가 아니라 문화**였지만, 실무에서는 "CI/CD + IaC + K8s + 클라우드 + 관측성"을 맡는 사람을 가리킴
2. **SRE, Platform Engineer, DevOps는 회사마다 정의가 다름.** 공고 내용을 꼭 읽을 것
3. **초급 DevOps → MLOps는 가장 짧은 길.** K8s/Terraform/관측성이 MLOps 스택의 70%
4. **자격증(CKA, AWS SAA)은 일본 채용에서 꽤 먹힘.** Phase 2 중 1~2개 확보 권장
5. **결국 "운영해본 경험"이 압도적.** 사이드 프로젝트를 반드시 K8s 위에서, Terraform으로, CI/CD 붙여서 운영할 것
