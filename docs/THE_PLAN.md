# THE PLAN — 6개월 일본 이직 실행서

> 이 문서 하나만 따라하면 된다. 다른 문서는 참고용.
> 기간: **24주 (6개월)**, 목표: **일본 자사 서비스 회사 주니어 인프라/SRE 엔지니어로 이직 + 이주**.

---

## 0. 현재 상태 스냅샷

| 항목 | 상태 |
|---|---|
| 나이 | 30세, 남 |
| 비자 | **배우자 비자(日本人の配偶者等) 가능** — 스폰서 불필요, 취업 제한 無 |
| 일본어 | N1 기취득(만료), 회화 약함, 청해 중상 |
| 영어 | 기본, 비즈니스 미달 |
| 경력 | 한국 IT 풀스택(잡부) 1년 미만 |
| 기술 | 백엔드 초급 / React 1년 미만 / DevOps 초급 / AI 전무 |
| 장기 방향 | DevOps 입사 → 1~2년 뒤 MLOps 전환 |

---

## 1. 타겟 회사 (합격 가능성 × 커리어 가치)

### 🎯 1순위: **Nulab** (후쿠오카 본사 / 도쿄 / 교토 / NY / 암스테르담)
- 제품: **Backlog / Cacoo / Nulab Pass** (글로벌 B2B SaaS, 180개국 400만 사용자)
- 직원 154명, 2004년 설립, **20년 자력 성장** (VC 의존 없음)
- 핵심 가치 **Nuice Ways**: Try First / Love Differences / Goal Oriented
- 채용 폴리시 **"국적·나이·성별 비평가"** 명시 → 외국인 진입 장벽 낮음
- **현재 공식 공고 0건**. 카주얼 면담 + 리퍼럴 창구 상시 열림:
  - 카주얼 면담: https://herp.careers/v1/nulab/uPb8iFlFjGZo
  - 리퍼럴: https://herp.careers/v1/nulab/E8bjhtcGUXtx
- 타겟 팀: **Reliability Engineering部**
- 채용사이트: https://careers.nulab.com/entry/

### 🛡 2순위 (백업, 병렬 지원)
| 순위 | 회사 | 지역 | 강점 |
|---|---|---|---|
| 2 | **Autify** | 도쿄 | AI QA SaaS, 영어 공용, 외국인 엔지니어 다수 |
| 3 | **Ubie** | 도쿄 | 헬스케어 AI, GCP+K8s, Global Team 영어 OK |
| 4 | **Cybozu** | 오사카/풀리모트 | K8s OSS(Neco) 유명, 리모트 친화 |
| 5 | **LINE Fukuoka** | 후쿠오카 | LY 계열, 한국인 다수(업무는 일본어) |

### ❌ 절대 배제 (SES/파견)
공고에 "客先常駐 / 派遣 / SES / 経験不問 / 未経験歓迎 / 연봉 하한 400만엔 미만 / 자사 제품명 없음 / 기술 블로그 없음" 하나라도 → 즉시 탈락.

---

## 2. 핵심 포트폴리오 — 단 하나의 프로젝트

### 프로젝트명: `infra-platform-demo`
**GitHub 공개 리포 1개**. 아래 요구사항 전부 포함.

```
[Terraform: AWS EKS (메인) + GCP GKE (READMEに併記)]
      ↓
[Kubernetes]
  ├─ FastAPI (Python) — 소규모 협업 API (Backlog 사용자 관점 영감)
  ├─ PostgreSQL (RDS / CloudSQL)
  ├─ vLLM Demo Pod — Llama 3 8B (차별화, 필수 아님 - M5부터)
  └─ React + TypeScript 프론트엔드
      ↓
[GitOps: ArgoCD]
      ↓
[CI/CD: GitHub Actions]  lint → test → build → push ECR → ArgoCD sync
      ↓
[Observability: Prometheus + Grafana + Alertmanager]
      ↓
[README: 영문 primary + 日本語 요약 + Cacoo로 그린 아키텍처 다이어그램 임베드]
```

### 필수 산출물
1. GitHub 공개 리포 (스타/포크 요청 NO, 그냥 공개)
2. **Cacoo 다이어그램** (Nulab 제품 사용 증명 = 면담 킬러)
3. **Qiita 일본어 블로그 3건**:
   - "EKSでvLLMを本番運用するTerraform構成"
   - "vLLMのPagedAttentionをOSのページングから理解する"
   - "Backlog Webhook + GitHub Actions でインフラPR自動化"
4. **Dev.to 영어 블로그 1건**: 프로젝트 overview
5. README 영/일 이중화 + 실행 가능한 setup 스크립트

### 원칙
- **깊이 > 넓이**. 이거 하나만 완성도 높게.
- vLLM 섹션은 마지막 차별화. 기초 인프라가 먼저.
- 모든 커밋은 의미 있는 메시지. 리포 히스토리가 포트폴리오의 일부.

---

## 3. 24주 주차별 커리큘럼 (재직 중 주 18~20h 기준)

### Phase 1: 기초 (W1~4) — 도구와 기반
| 주 | 기술 | 언어 | 산출물 |
|---|---|---|---|
| W1 | Linux/Bash (MIT Missing Semester 1~3강), Git 심화, GitHub 리포 `mlops-learning` 공개 | 영어 리스닝 루틴 시작 (Lex Fridman 30분/일), italki 영어 튜터 트라이얼 2명 | Wantedly + LinkedIn 프로필 일/영 작성 |
| W2 | Docker 완전 이해 (namespace/cgroups/레이어), 공식 Get Started | italki 영어 주 2회 고정, 일본어 튜터 트라이얼 | FastAPI 앱 Docker 이미지 빌드 및 Hub 푸시 |
| W3 | Python 자동화 스크립트 3개 (로그 파싱, API 호출, K8s 리소스 조회) | 일본어 튜터 주 2회 고정, 배우자 매일 30분 통화 시작 | Python 스크립트 GitHub 공개 |
| W4 | Kubernetes 기초: kind 로컬 멀티노드, Pod/Deployment/Service/Ingress/ConfigMap/Secret | | `infra-platform-demo` 리포 생성, FastAPI를 kind에 배포 |

### Phase 2: 클라우드 + IaC (W5~8)
| 주 | 기술 | 언어 | 산출물 |
|---|---|---|---|
| W5 | AWS 기초 (VPC/EC2/EKS/S3/IAM/ECR/RDS), AWS Skill Builder 무료 코스 | 영어 자기소개 90초 스크립트 완성 | AWS 계정 + VPC 수동 구성 |
| W6 | Terraform 기초: AWS provider, state, module 개념 | 일본어 자기소개 90초 스크립트 완성 | Terraform으로 VPC/Subnet/EKS 클러스터 프로비저닝 |
| W7 | K8s 심화: Helm, HPA, RBAC, NetworkPolicy, Ingress 컨트롤러 | italki 일/영 각 주 2회 유지 | FastAPI를 EKS에 배포, Helm chart 작성 |
| W8 | **Cacoo로 아키텍처 다이어그램** 완성, README 영/일 초안 | | **Cacoo 다이어그램 임베드 완료** |

### Phase 3: 자동화 + 관측성 (W9~12)
| 주 | 기술 | 언어 | 산출물 |
|---|---|---|---|
| W9 | GitHub Actions 파이프라인 (lint → test → build → push ECR) | LeetCode Easy 주 3문제 시작 | CI 완성 |
| W10 | ArgoCD 도입 (GitOps), Helm chart 자동 sync | **HashiCorp Terraform Associate (003) 응시·합격** (비용 $70·60분, W6~W9 학습한 Terraform 지식으로 충분) | GitOps 완성, **Terraform Associate 취득** |
| W11 | Prometheus + Grafana, ServiceMonitor, kube-state-metrics | Qiita 블로그 **1건째 공개** (CI/CD 경험담) | 대시보드 2개 (앱 메트릭 + 클러스터) |
| W12 | Alertmanager, Slack 연동, RunBook 작성 | | 관측성 스택 완성, **체크포인트: 여기까지 완성 못 했으면 9개월로 일정 연기** |

### Phase 4: 차별화 + 비자 + 자격 (W13~16)
| 주 | 기술 | 언어 | 산출물 |
|---|---|---|---|
| W13 | vLLM 로컬 실행 (RunPod GPU 시간당 $0.5), Llama 3 8B 서빙 | **배우자 비자 신청 착수 (在留資格認定証明書)** — 이 주차가 데드라인 | vLLM Docker 이미지 |
| W14 | vLLM을 EKS GPU 노드에 배포, K8s Device Plugin 이해 | PagedAttention 논문 정독 + OSTEP Ch.18~22 | vLLM on EKS 작동 |
| W15 | **CKA 시험 예약 확정 (W16 날짜)** + Killer.sh 시뮬레이터 구매/연습 | Qiita 블로그 **2건째 공개** (PagedAttention + OS 페이징) | |
| W16 | **CKA 응시 + 합격** | 영문 Resume + 日本語 職務経歴書 완성 (CKA 반영) | **CKA 취득**, Resume 2종 완성 |

### Phase 5: 지원 + 면담 (W17~20)
| 주 | 액션 |
|---|---|
| W17 | **Nulab 카주얼 면담 신청** (섹션 4 메시지 사용), Autify/Ubie/Cybozu 공식 지원, LinkedIn에서 Nulab 현직자 5명 connect |
| W18 | Wantedly 追加 지원 3곳 (Hatena, Money Forward Fukuoka/Osaka, LINE Fukuoka), Nulab 블로그에 월 2건 사려깊은 코멘트 시작 |
| W19 | 1차 기술 면접 시작 (영어 코딩 면접: LeetCode Easy 30 완료 기준), 일본어 모의 면접 주 2회, **AWS SAA-C03 응시** (이력서 추가 탄환) |
| W20 | Qiita 블로그 **3건째 공개** (Backlog Webhook + Terraform), Nulab 카주얼 면담 실전, 면담 24h 내 감사 메시지 |

### Phase 6: 최종 면접 + 이주 (W21~24)
| 주 | 액션 |
|---|---|
| W21 | 2차/3차 면접 (시스템 디자인 + 행동 면접), 오퍼 협상 준비 |
| W22 | 오퍼 수령 (목표 연봉 550~750만엔), 현 회사 퇴사 통보 (2주 전 통보 규정 확인) |
| W23 | 이주 물류 (주택 해약, 은행, 항공권, 짐), 배우자 비자 수령 확인 |
| W24 | 일본 입국 → 주소 등록 → 입사 |

---

## 3A. AI/ML 병렬 트랙 (주 2~3h, 24주 전체 상시)

> 목적: DevOps 취업 스프린트와 **병렬로 ML 기초 축적** → 면접에서 "MLOps 지향이 말뿐이 아니다"를 증명. 이주 후 1~2년차 MLOps 전환 가속.
> 시간 배분: **주 2~3h 이하 엄수.** DevOps 본 트랙(15h)을 절대 잠식하지 말 것.
> 산출물 원칙: **작게 자주 커밋**. 각 주차 끝에 GitHub `ai-learning` 서브디렉토리에 결과물 1개.

### 트랙 구조 (6단계)
```
W1~4   : Python ML 토대 (numpy/pandas/sklearn, Jupyter)
W5~8   : PyTorch 기초 + HuggingFace Transformers
W9~12  : LLM 내부 구조 + 로컬 LLM 운영 (Ollama/llama.cpp)
W13~16 : vLLM + PagedAttention (메인 커리큘럼과 통합)
W17~20 : MLOps 도구 (MLflow, Kubeflow 개요, 모델 서빙 패턴)
W21~24 : 면접용 정리 + 블로그화
```

### Phase AI-1 (W1~4): Python ML 토대
| 주 | 내용 | 시간 | 산출물 |
|---|---|---|---|
| W1 | numpy/pandas 기초 (Kaggle Learn 무료 2코스) | 2h | 간단한 데이터 분석 노트북 1개 |
| W2 | matplotlib/seaborn 시각화 + Jupyter 환경 | 2h | 데이터 EDA 노트북 |
| W3 | scikit-learn: 회귀/분류 기본, train/test split, 교차검증 | 3h | Iris or Titanic 데이터로 분류 모델 1개 |
| W4 | HuggingFace Hub 둘러보기, `pipeline()` API 사용 (감정분석/요약) | 2h | **감정분석 API를 FastAPI에 붙이기** (포트폴리오에 통합 가능) |

### Phase AI-2 (W5~8): PyTorch + Transformers
| 주 | 내용 | 시간 | 산출물 |
|---|---|---|---|
| W5 | PyTorch 공식 60분 튜토리얼 (Tensor, Autograd, Module) | 2h | 노트북 완주 |
| W6 | PyTorch로 MNIST 직접 학습 (CNN) | 3h | 훈련 스크립트 + 체크포인트 |
| W7 | HuggingFace Transformers 라이브러리 구조 (Tokenizer/Model/Trainer) | 2h | BERT 소형 모델 파인튜닝 1회 (감정분석) |
| W8 | 모델을 Docker로 패키징, FastAPI로 추론 API 노출 | 3h | **Docker 이미지 → `infra-platform-demo`에 마이크로서비스로 통합** |

### Phase AI-3 (W9~12): LLM 내부 구조 + 로컬 운영
| 주 | 내용 | 시간 | 산출물 |
|---|---|---|---|
| W9 | Transformer 아키텍처 개요 (Attention, Self-Attention, Positional Encoding) | 2h | 개념 정리 노트 (일본어 블로그 소재) |
| W10 | Tokenization (BPE, SentencePiece), KV 캐시 개념 | 2h | 토크나이저 실험 노트북 |
| W11 | **Ollama / llama.cpp** 로 로컬 LLM 실행 (Llama 3 8B 양자화 버전) | 3h | 로컬 챗 데모 (CLI) |
| W12 | 로컬 LLM을 API 서버로 노출, 간단 RAG 데모 | 3h | **RAG 챗봇 프로토타입** → K8s 배포 가능한 컨테이너 |

### Phase AI-4 (W13~16): vLLM + PagedAttention (본 커리큘럼과 통합)
*본 섹션은 메인 커리큘럼 W13~16에 이미 포함. 중복이 아니라 같은 작업을 양쪽에서 인식.*

| 주 | 내용 | 시간 | 산출물 |
|---|---|---|---|
| W13 | vLLM 로컬 실행, HF 모델 로드, throughput/latency 측정 | 3h | 벤치마크 노트 |
| W14 | vLLM을 EKS GPU 노드에 배포 (NVIDIA Device Plugin) | 3h | K8s 매니페스트 |
| W15 | PagedAttention 논문 정독 + OSTEP Ch.18~22와 매핑 | 3h | Qiita 블로그 2건째 |
| W16 | vLLM `block_manager.py` 코드 리딩 + 블록 사이즈 실험 | 2h | 블로그 draft |

### Phase AI-5 (W17~20): MLOps 도구 개요
| 주 | 내용 | 시간 | 산출물 |
|---|---|---|---|
| W17 | **MLflow** 기초: experiment tracking, model registry (로컬 구동) | 2h | 이전 학습 실험들 MLflow에 로깅 |
| W18 | Kubeflow 개요 영상 2편 + 공식 아키텍처 문서 정독 | 2h | 개념 정리 (면접용 설명 5분) |
| W19 | 모델 서빙 패턴 (vLLM vs Triton vs TGI vs Ollama) 비교 | 2h | 비교표 → 면접 시 답변 자산 |
| W20 | Feature Store 개념 (Feast 공식 문서) + 데이터 드리프트 개요 | 2h | 개념 노트 |

### Phase AI-6 (W21~24): 면접용 정리 + 블로그화
| 주 | 내용 | 시간 | 산출물 |
|---|---|---|---|
| W21 | 전체 AI/ML 학습 내용 면접 답변 스크립트화 (일/영 양쪽) | 2h | "AI/ML 경험" 3분 설명 2개 국어 |
| W22 | MLOps 관점 발표 자료 1장 (Google Slides) | 2h | 면접 제출용 |
| W23 | 이주 집중, 학습은 최소 (2h) | 2h | 기존 블로그 리뷰 |
| W24 | 입사 후 1일차: 사내 ML 팀 유무 확인, 접촉 루트 탐색 | — | 사내 네트워킹 시작 |

### AI 트랙 교재 (전부 무료 or 저가)
| 자료 | 링크 | 용도 |
|---|---|---|
| Kaggle Learn | https://www.kaggle.com/learn | Python/Pandas/ML 기초 무료 |
| PyTorch 공식 Tutorials | https://pytorch.org/tutorials/ | PyTorch 전반 |
| HuggingFace NLP Course | https://huggingface.co/learn/nlp-course | Transformers 실전 |
| Andrej Karpathy "Let's build GPT" | https://www.youtube.com/watch?v=kCc8FmEb1nY | Transformer 깊이 이해 (우선순위 중) |
| Attention Is All You Need | https://arxiv.org/abs/1706.03762 | 원논문, W9에 읽기 |
| PagedAttention 논문 | https://arxiv.org/abs/2309.06180 | W15 필독 |
| vLLM 공식 문서 | https://docs.vllm.ai/ | W13~16 레퍼런스 |
| MLflow docs | https://mlflow.org/docs/latest/ | W17 |
| Kubeflow docs | https://www.kubeflow.org/docs/ | W18 |

### GPU 리소스 예산
| 시점 | 리소스 | 비용 |
|---|---|---|
| W5~W8 | Google Colab Free Tier (MNIST/BERT 파인튜닝) | $0 |
| W11~W12 | 로컬 CPU (Ollama 양자화 모델 7B까지) | $0 |
| W13~W16 | **RunPod GPU spot (RTX 4090 or A10)** 주 5h × 4주 = 20h | 시간당 $0.4~$0.7 → 약 **$15~20** |
| W17~W20 | 필요 시 RunPod 추가 수시 | $10 예산 |
| **합계** | | **약 $30~40 (5만 원)** |

### AI 트랙 통합 원칙
1. **W4, W8, W12의 산출물은 `infra-platform-demo` 포트폴리오에 마이크로서비스로 병합** — 별도 리포 아님. 감정분석 API, RAG 챗봇, vLLM 서빙 전부 한 클러스터에 배치
2. **Qiita 블로그 3건 중 1건은 AI/ML 주제로** (이미 계획된 PagedAttention 블로그가 이 역할)
3. **면접 답변**: "DevOps 지원자이지만 MLOps 방향을 향해 이미 파이썬부터 vLLM까지 한 포트폴리오에 통합했다" → Nuice Ways의 **Try First** 증거
4. **시간 초과 금지**: 주 3h 넘으면 AI 트랙이 DevOps를 잠식. 스프린트 원칙 무너짐

### AI 트랙 체크포인트
| 시점 | 필수 | 미달 시 |
|---|---|---|
| W4 | sklearn 모델 1개 + HF pipeline API 사용 | W1~4 다시 |
| W8 | PyTorch로 모델 1개 학습 + Docker 패키징 | AI 트랙 난이도 하향 (vLLM 데모까지만) |
| W12 | 로컬 LLM 실행 + RAG 프로토타입 | vLLM 단계 스킵, W13~16만 유지 |
| W16 | vLLM on EKS 작동, PagedAttention 블로그 공개 | 필수. 미달 시 AI 면접 어필 포기 |
| W20 | MLOps 도구 개요 면접 설명 가능 | 면접 시 AI 주제 자신있게 꺼내지 말 것 |

### 금지 사항 (AI 트랙 전용)
1. **논문 과잉 읽기** — W9 Transformer 원논문, W15 PagedAttention 딱 2개만 정독
2. **Kaggle 대회 참가** — 시간 블랙홀
3. **Fine-tuning 깊게 파기** — W7의 1회면 충분, LoRA/QLoRA는 이주 후
4. **RLHF/Constitutional AI 이론 심화** — 6개월 스프린트 범위 밖
5. **최신 SOTA 논문 추적** — ArXiv 덕질 금지

---

## 4. Nulab 공략 플레이북 (1순위 전용)

### 4-1. 사전 준비 (W1부터 상시)
- [ ] **Backlog 무료 트라이얼 가입**, 실제 1개월 이상 사용. 팀 프로젝트 관리 시나리오로 사용할 것
- [ ] **Cacoo로 `infra-platform-demo` 아키텍처 다이어그램 작성** → README에 임베드
- [ ] Nulab 엔지니어링 블로그 10건 정독 (https://nulab.com/blog/ + /ja/blog/)
- [ ] Reliability Engineering 관련 포스트 3건 식별 + 메모
- [ ] GitHub @nulab 상위 리포 5개 클론 후 README 정독
- [ ] LinkedIn에서 Nulab Reliability Engineering 직함 5명 이상 식별

### 4-2. Nuice Ways 3축 — 모든 커뮤니케이션에 녹일 것

| 가치 | 내 스토리 앵커 |
|---|---|
| **Try First** | 풀스택 잡부 → 자발적 DevOps/MLOps 로드맵 설계, 6개월 포트폴리오, PagedAttention을 OS 페이징으로 이해한 접근 |
| **Love Differences** | 한국인 + 일본인 배우자 다문화 가정, Nulab NY/암스테르담 오피스와 협업 적합성, 한일 IT 문화 브릿지 |
| **Goal Oriented** | 커리어 계획을 문서화한 공개 레포(= 이 문서), 본질 탐구형 전환(MLOps 지향) |

### 4-3. 카주얼 면담 신청 메시지 (일본어 원문)

```
Nulabのカジュアル面談に応募させていただきます。

韓国ソウル在住のフルスタックエンジニアで、2026年Q4に配偶者ビザで
日本（福岡または東京）に移住予定です。

Nulabに惹かれた理由:
- 福岡発、150名規模で20年以上グローバルSaaSを運営されている
  ユニークなポジション
- 採用ポリシーで国籍や年齢を評価対象外と明示されている姿勢
- Reliability Engineering部が、Backlog/Cacooのような180カ国
  ユーザー向けSaaSのスケールを支えている点

学習状況:
- Terraform + AWS EKS + ArgoCD によるインフラポートフォリオ構築中
- アーキテクチャ図は実際にCacooで作成しました
- GitHub: https://github.com/[ID]/infra-platform-demo
- Qiitaで関連する技術ブログを継続発信中

将来的にはMLOps領域に進みたく、その前段階としてPlatform/SREの
運用経験を積みたいと考えております。

Reliability Engineering部の方とお話しできれば幸いです。
日本語・英語どちらでも対応可能です。
```

### 4-4. 카주얼 면담 실전 (30분)
**25분 듣기 : 5분 질문**. 아래 질문 2~3개만 던져도 인상 남김:
1. Reliability Engineering 팀이 지금 직면한 가장 큰 기술 챌린지는?
2. Backlog의 멀티 리전 운영에서 K8s는 어디까지 쓰이나요?
3. 최근 1년간 팀 규모 변화는? (채용 의향 탐색)
4. 새로 들어온 멤버가 가장 빠르게 기여하는 영역은?
5. **마지막 필수 질문**: "공고가 오픈되면 어떻게 알 수 있을까요?"

### 4-5. 존재감 유지 (W20~)
- 월 1회 Qiita 블로그 (Nulab 제품 연관 주제)
- X에서 @nulabinc 멘션하며 블로그 공유
- Nulab 공식 블로그 신규 포스트에 월 2건 사려깊은 코멘트
- 면담에서 만난 엔지니어에게 2개월 간격 근황 업데이트

### 4-6. 공고 오픈 시 → **24시간 내 지원**
`careers.nulab.com/entry/` 주 1회 체크. 리퍼럴 라인이 있으면 리퍼럴 경유.

---

## 5A. 자격증 로드맵

> 원칙: **"면접에서 보여줄 수 있는 증거 + 일본 이력서의 시각적 시그널"** 목적. 과다 취득 금지 (시간 낭비).
> 일본 채용은 자격증 가점 명시 회사 많음(특히 Rakuten/Cybozu/LINE Fukuoka 스타일). Nulab은 기술 면접 비중이지만 CKA 있으면 눈에 띔.

### 5A-1. 6개월 안에 반드시 취득 (3종)

| 우선 | 자격증 | 시점 | 비용 | 공부 시간 | 비고 |
|---|---|---|---|---|---|
| ★1 | **CKA** (Certified Kubernetes Administrator) | W16 | $395 (세일 시 $316) | 80~100h (포트폴리오와 중복) | **최우선**. K8s 실력 직접 증명. Nulab/Autify/Ubie/Cybozu 전부 가산. Killer.sh 시뮬 2회 필수 |
| ★2 | **HashiCorp Terraform Associate (003)** | W10 | $70·60분 | 20~30h | 저비용 고효율. W6~W9 포트폴리오 공부와 거의 중복 → 공짜로 따는 셈 |
| ★3 | **AWS SAA-C03** (Solutions Architect Associate) | W19 | $150 | 60~80h | 일본 채용에서 가장 널리 인정. Autify/Ubie/Money Forward 가산 |

**이 3종 = 이력서에 "K8s + IaC + Cloud" 삼각편대 완성.** Nulab `infra-platform-demo` 포트폴리오의 기술 스택을 자격증으로 재인증하는 구조.

### 5A-2. 일본어 자격 — JLPT N1 재취득 전략

**현재 N1 만료 (유효기간 개념은 공식엔 없으나 이력서 신뢰도 하락)**

| 옵션 | 시기 | 판단 |
|---|---|---|
| A. 6개월 안에 재응시 안 함 | — | **권장**. 스프린트 기간은 회화 복구에 집중. 이력서엔 "N1 取得 (2020年)" 로 기재 |
| B. 2026년 7월 JLPT 재응시 | W13경 | 한국에서 응시 가능. 시간 뺏김. **비권장** |
| C. 이주 후 2026년 12월 재응시 | 이주 후 | **권장**. 일본 거주 중 응시 → 이력서에 최신 일자로 갱신 |

**대안: BJT (ビジネス日本語能力テスト) J2 이상** — 비즈니스 일본어 특화, 연중 수시 응시 가능. 이주 후 3~6개월 내 응시 고려.

### 5A-3. 영어 자격 — 필요 시점에만

일본 채용은 TOEIC 중심. Nulab은 영어 스피킹 직접 평가라 점수 무의미.

| 자격 | 필요 여부 | 비고 |
|---|---|---|
| TOEIC 800+ | Rakuten/대형 일본계 지원 시에만 | Nulab/Autify/Ubie는 불필요. 이 스프린트에선 응시 안 함 |
| IELTS/TOEFL | 불필요 | 일본 IT 채용 거의 무의미 |

→ **이 스프린트에선 영어 자격증 생략**. 영어는 면접에서 회화로 증명.

### 5A-4. 한국 자격증 — 기본 점검

| 자격 | 일본 인지도 | 조치 |
|---|---|---|
| 정보처리기사 | **무의미** (일본 기업 대부분 모름) | 있으면 이력서에 "Engineer Information Processing (Korea National Cert)" 라고 영문 기재 1줄. 없으면 굳이 따지 말 것 |
| SQLD/SQLP | 무의미 | 시간 낭비 |
| 리눅스마스터 2급 | 무의미 | LPIC가 훨씬 유효 |

→ **기존에 정보처리기사 있으면 기재만, 없으면 패스.**

### 5A-5. 이주 후 취득할 자격증 (1~2년차 플랜)

**일본 입사 후 현업 병행**. MLOps 전환 가속용.

| 시기 | 자격증 | 이유 |
|---|---|---|
| +3~6개월 | **応用情報技術者 (AP)** 또는 基本情報技術者 (FE) | IPA 국가자격. 일본 SIer/엔터프라이즈 채용엔 필수급. **정보처리기사 대체재**. 4월/10월 시험, 상반기 CBT도 있음 |
| +6~9개월 | **CKAD** (Certified Kubernetes Application Developer) | CKA 취득자 할인. 앱 개발 관점 K8s 증명 |
| +9~12개월 | **AWS DevOps Engineer Professional** or **GCP Professional Cloud DevOps Engineer** | 회사 스택에 맞춰 선택 (Autify/Cybozu면 AWS, Ubie면 GCP) |
| +12~18개월 | **CKS** (Certified Kubernetes Security Specialist) | K8s 3관 완성, 연봉 협상 카드 |
| +18~24개월 | **Google Professional Machine Learning Engineer** or **AWS ML Specialty** | MLOps 전환 시점. Rakuten GPUOD/PFN 지원 전 탄환 |

### 5A-6. MLOps 특화 자격 (Phase 3, 2~3년차)

| 자격 | 비고 |
|---|---|
| **Google Professional ML Engineer** | GCP 기반 MLOps. Ubie 내부 이동 또는 외부 전직 |
| **AWS ML Specialty** | AWS 기반, 2024 리뉴얼 |
| **Databricks ML Associate** | 2025~ 일본에서 존재감 확대 |
| **Prometheus Certified Associate (PCA)** | 관측성 심화. SRE/MLOps 양쪽에 유효 |
| **Kubestronaut 인증** | CKA+CKAD+CKS+KCNA+KCSA 5관. 채용 시장 최상위 시그널 |

### 5A-7. 자격증 예산 (6개월 스프린트)

| 항목 | 비용 |
|---|---|
| CKA + Killer.sh 시뮬 | $395 + $36 = **$431** |
| Terraform Associate | **$70** |
| AWS SAA-C03 | **$150** |
| (옵션) CKA 재시험 무료 포함 |  |
| **합계** | **약 $651 (약 100만 원)** |

**재시험 대비**: CKA 1회 무료 재시험 포함. SAA/Terraform 실패 시 재응시 비용 추가.

### 5A-8. 이력서 기재 포맷

**영문 Resume Certifications 섹션**
```
CERTIFICATIONS
- Certified Kubernetes Administrator (CKA) — 2026
- AWS Certified Solutions Architect Associate (SAA-C03) — 2026
- HashiCorp Certified: Terraform Associate (003) — 2026
- JLPT N1 (Japanese-Language Proficiency Test, Level 1) — 2020
```

**日本語 職務経歴書 資格 섹션**
```
保有資格
- Certified Kubernetes Administrator (CKA) : 2026年X月取得
- AWS認定 ソリューションアーキテクト – アソシエイト (SAA-C03) : 2026年X月取得
- HashiCorp Certified: Terraform Associate (003) : 2026年X月取得
- 日本語能力試験 N1 : 2020年取得 (移住後再取得予定)
```

### 5A-9. 자격증 금지 사항

1. 6개월 안에 **4개 이상 시도 금지** (CKA/Terraform/SAA 3종으로 고정)
2. CKS/CKAD를 CKA 전에 시도 금지
3. 일본 현지 국가자격 (FE/AP) 한국에서 응시 금지 — 일본 이주 후
4. Docker Certified Associate (DCA), Linux Foundation 유료 강의 번들 — 시간 대비 효율 낮음
5. "대충 훑어보고 응시" 금지 — 불합격 시 재시험 비용·일정 밀림

---

## 5. 언어 전략

### 타협 없음: 영어 **비즈니스**, 일본어 **생활 + 면담**
- 타겟 회사 절반 이상이 영어 공용 또는 영어 OK 팀
- 일본어는 정착 + 팀 일상 + 면담 친화용으로 필요, 비즈니스 수준 요구는 덜함

### 매일 고정 루틴
| 시간대 | 내용 | 시간 |
|---|---|---|
| 아침 출근 길 | 영어 팟캐스트 (Lex Fridman / Changelog) | 30분 |
| 점심 | NHK Easy News 음독 | 10분 |
| 저녁 학습 중 | 기술 자료는 영어 원문 우선 | — |
| 밤 | 배우자와 일본어 통화 | 30분 |
| 주 2회 | italki 영어 기술 튜터 | 각 45분 |
| 주 2회 | italki 일본어 비즈니스 튜터 | 각 45분 |

**금지**: 일본어 쉬는 날, 영어 쉬는 날 없음. 기술은 쉬어도 언어는 매일.

### 자기소개 3종 (암기 필수, W5~W6 완성)
1. **영어 90초** — 기술 포지셔닝 + 일본 이주 이유 + 포트폴리오 요약
2. **일본어 90초** — 위와 동일, 배우자/비자 언급
3. **Nulab 맞춤 90초** — Nuice Ways + Backlog/Cacoo 사용 경험

---

## 6. Resume / 職務経歴書 템플릿

### 영문 Resume (1페이지)
```
[Name] | [City] → Relocating to Japan (Spouse Visa) | [email] | github.com/[id]

SUMMARY
Full-stack engineer transitioning to platform/SRE, with production-
focused portfolio on Kubernetes and Terraform. Planning relocation
to Japan Q4 2026.

TECHNICAL SKILLS
Languages: Python, TypeScript, Bash
Infrastructure: AWS (EKS, VPC, IAM, RDS), Terraform, Kubernetes,
  Docker, Helm, ArgoCD
CI/CD & Observability: GitHub Actions, Prometheus, Grafana
Certifications: CKA (2026), AWS SAA-C03 (2026), HashiCorp Terraform Associate (2026), JLPT N1 (2020)

SELECTED PROJECT
infra-platform-demo — [github link]
  End-to-end platform: Terraform-provisioned EKS, GitOps via ArgoCD,
  observability stack, vLLM inference demo.
  Architecture documented in Cacoo, deep-dive blogs on Qiita (JP).

EXPERIENCE
[Current Company] | Full-stack Engineer | 2024–2026
  - Shipped features across React frontend, Python/Node backend,
    AWS infrastructure
  - Introduced GitHub Actions CI pipeline reducing deploy errors

EDUCATION
[University] | [Major] | [Year]

LANGUAGES
Japanese: N1 (2020), conversational. English: business working level.
```

### 日本語 職務経歴書 (3페이지 표준)
1페이지: 職務要約 + 活かせるスキル/知識
2페이지: 職務経歴 (회사별 기간, 역할, 담당 업무, 성과, 기술)
3페이지: 自己PR (Nuice Ways 3축 + 이주 계획 + 장기 비전)

**필수 문구**:
- "配偶者ビザを保有予定、2026年Q4頃に日本移住を予定"
- "日本語: JLPT N1取得 (日常・ビジネス会話可)、英語: ビジネスレベル"

---

## 7. 비자 + 이주 타임라인

```
W13: 배우자 일본에서 在留資格認定証明書 신청 (입관국)
W17~20: 증명서 발급 (보통 1~3개월)
W21: 증명서를 주일본대사관에 제출, 배우자 비자 발급
W22: 오퍼 수령 후 현 회사 퇴사 통보
W23: 이주 물류
W24: 입국 + 주소 등록 + 입사
```

### 배우자 비자 필요 서류 (배우자 준비)
- 재류자격인정증명서 교부신청서
- 혼인 증명 (양국 서류)
- 배우자(일본인)의 호적등본, 주민표
- 배우자의 수입 증명 (과세증명서 / 재직증명서)
- 질문서, 사진, 스냅샷

**지금 이번 주 배우자와 서류 리스트 합의 필수.**

---

## 8. 주간 루틴 템플릿

### 평일 (월~금, 하루 2.5~3h 학습)
| 시간대 | 내용 |
|---|---|
| 출근 30분 | 영어 팟캐스트 |
| 저녁 90~120분 | 그 주 DevOps 기술 토픽 (Phase별 커리큘럼) |
| 화/목 추가 45분 | italki 튜터 (영/일 교차) |
| 점심 10분 | NHK Easy News |
| 밤 30분 | 배우자 일본어 통화 |

### 주말
| 요일 | 블록 | 내용 |
|---|---|---|
| 토 오전 4h | 포트폴리오 구현 집중 (DevOps 본 트랙) |
| 토 오후 1h | 블로그 드래프트 |
| 일 오전 2h | 포트폴리오 구현 or 자격시험 공부 |
| **일 오후 2~3h** | **AI/ML 병렬 트랙 (섹션 3A)** ← 집중 블록 |
| 일 저녁 1h | 공고 수집 + LinkedIn 활동 + Nulab blog 코멘트 |

**주 총합: 20~24h** (DevOps 15h + AI 2~3h + 언어 4h + 활동 1h)

### 트랙별 시간 배분 원칙
| 트랙 | 주 시간 | 비고 |
|---|---|---|
| DevOps 본 트랙 (포트폴리오 + 공부) | 15h | 절대 타협 금지 |
| AI/ML 병렬 트랙 | 2~3h | **일요일 오후 고정 블록**, 초과 금지 |
| 언어 (영/일) | 4h | 매일 분산, 쉬는 날 없음 |
| 자격증 대비 | 기존 DevOps/AI 시간 내 흡수 (별도 추가 X) | W10/W16/W19 직전 2주간만 집중 |
| 구직 활동 | 1~2h (W17부터 3~4h로 증가) | |

---

## 9. 체크포인트 (미달 시 즉시 일정 조정)

| 시점 | 필수 | 미달 시 |
|---|---|---|
| W4 | Docker/K8s 기초 OK, Wantedly + LinkedIn 프로필 완성 | 이주 +1개월 |
| W8 | Terraform + EKS 작동, Cacoo 다이어그램 완성 | 포트폴리오 단순화 |
| W12 | CI/CD + 관측성 전부 작동, 블로그 1건 공개 | **9개월 플랜으로 재조정** |
| W16 | 비자 신청 완료, Resume 2종, CKA 합격 | 비자 지연이면 W24 → W28 조정 |
| W20 | 10곳 이상 지원 + Nulab 카주얼 면담 완료 | 타겟 풀 +10곳 확장 |
| W24 | 오퍼 수령 + 이주 준비 완료 | 한국 재직 유지, 매월 추가 지원 |

---

## 10. 면접 예상 질문 Top 20 + 모범 답 각도

### 기술 (영어/일본어 양쪽)
1. **What is the difference between a Deployment and a StatefulSet?** → stateful 데이터 + stable network identity
2. **How would you debug a pod stuck in CrashLoopBackOff?** → logs → describe → events → exec → image/config
3. **What does Terraform state do? What happens if it's corrupted?** → 리소스 매핑, backup restore, import 재구성
4. **Explain PagedAttention simply.** → OS 페이징의 KV 캐시 적용, 외부 단편화 제거
5. **How do you set up a CI pipeline from scratch?** → lint/test/build/security-scan/push/deploy 단계
6. **What's the difference between SLI/SLO/SLA?** → 측정/목표/계약
7. **How does K8s schedule a GPU pod?** → Device Plugin + nodeSelector/tolerations
8. **What's a headless Service?** → clusterIP: None, DNS 직접 Pod IP
9. **Explain blue-green vs canary deployment.** → 스위칭 방식 vs 점진적 트래픽
10. **What's Helm's benefit over raw manifests?** → 템플릿화, 값 분리, 버전 관리

### 행동 (일본어 특히)
11. "どうして日本で働きたいですか？" → 배우자 + 커리어 전환 진정성
12. "なぜNulab（또는 Autify등）ですか？" → 구체적 이유 3개 (회사별 준비)
13. "最近挑戦したことは？" → Try First 스토리 (포트폴리오 제작기)
14. "チームで意見が割れた経験は？" → Goal Oriented (본질 논의)
15. "文化が違う相手と仕事した経験は？" → Love Differences (다문화 가정 + 한일 경험)
16. "なぜフルスタックからSRE/Platformへ？" → 본질 + 장기 비전 (MLOps)
17. "5年後のキャリアイメージ？" → MLOps 전환 솔직하게 (단, 이 회사에서의 기여 전제로)
18. "弱みは？" → 일본어 비즈니스 회의는 복구 중 (대책 포함)
19. "逆質問？" → 섹션 4-4 질문 5개
20. "なぜ今の会社を辞めるのか？" → 다음 성장 기회 + 가족 이주 (긍정 프레임)

---

## 11. 이번 주 착수 체크리스트 (7일 안)

- [ ] 배우자와 **이주 시점 W24 (6개월 후) 최종 합의**, 비자 서류 리스트 공유
- [ ] GitHub 리포 `mlops-learning` 공개 (이 docs 포함)
- [ ] GitHub 리포 `infra-platform-demo` 생성 (placeholder README)
- [ ] Wantedly 계정 생성, 일본어 프로필 초안 (배우자 비자 + 이주 일정 명시)
- [ ] LinkedIn 프로필 영문 정비, "Open to Work" 비공개 ON (채용 담당자에만 표시)
- [ ] italki 튜터 트라이얼 예약: 영어 기술 2명, 일본어 비즈니스 2명
- [ ] Docker 공식 Get Started 1~3장 완료
- [ ] **Backlog 무료 트라이얼 가입**, 실제 프로젝트 만들어서 사용 시작
- [ ] Nulab careers + blog 북마크, RSS 구독 설정
- [ ] Nulab LinkedIn 현직자 5명 식별하여 팔로우
- [ ] **Linux Foundation 계정 생성** (CKA 응시 준비) + **HashiCorp Learn 계정** + **AWS Training 계정**
- [ ] CKA 시험 일정 W16으로 가예약 확인 (응시 바우처 세일 타이밍 모니터링)
- [ ] 기존 보유 자격증 전수 점검 (정보처리기사/SQLD 등) → Resume 영문/일문 기재 여부 결정
- [ ] **Kaggle 계정 생성** + **HuggingFace 계정 생성** (AI 트랙 W1 시작용)
- [ ] **Google Colab 접속 확인** (무료 GPU 환경 테스트)
- [ ] RunPod 계정 생성 (W13 GPU 예산 집행 대비)
- [ ] AI 트랙 일요일 오후 2~3h 블록을 캘린더에 고정 (DevOps 본 트랙 침범 금지)

---

## 12. 금지 사항

1. "未経験歓迎" 공고 지원 — 전부 SES. 시간 낭비
2. 여러 포트폴리오 분산 제작 — `infra-platform-demo` 1개에 집중
3. 일본어 공부 쉬는 날 — 금지. 피곤하면 5분만이라도
4. Nulab에만 매달리기 — 병렬 지원 의무 (Autify/Ubie/Cybozu)
5. AI/ML 트랙이 주 3h 초과 — DevOps 본 트랙 잠식 금지. 6개월 안은 vLLM 데모 수준까지만. LoRA/RLHF/SOTA 추적 금지
6. LeetCode Medium/Hard 과잉 — Easy 30문제로 충분
7. 자격증 4종 이상 시도 — CKA + Terraform Associate + AWS SAA 3종 고정, CKS/CKAD/TOEIC 유혹 금지
8. 스터디 자료 과다 구매 — OSTEP + K8s 공식 문서 + 기본 유료 코스 1개 정도
9. "완벽한" Resume 고집 — W16에 v1 완성 후 지원하며 반복 개선
10. Nulab 공고 개설 기다리기만 — 병렬 지원 필수

---

## 13. 이 문서의 운영

- **매주 일요일 저녁 30분**: 이번 주 체크리스트 진척, 다음 주 플랜 확인
- **매월 1일**: Nulab 공고 재확인, 체크포인트 갱신
- 플랜 변경 시 이 문서 직접 수정. 별도 플랜 문서 신설 금지.

---

## 끝 — 시작해라.
