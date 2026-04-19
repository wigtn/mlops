# MLOps 엔지니어 심층 이해 레포

> 목적: "MLOps 엔지니어가 도대체 뭐하는 사람인가"를 스스로 설명할 수 있을 때까지 정리.
> DevOps는 수단/기반이고, **모델과 데이터가 추가로 들어오는 순간 무엇이 달라지는가**에 집중.
> `devops-deep-dive.md` 의 자매편. 이주 후 1~2년차 전환 시기에도 계속 참조.

---

## 1. MLOps란 무엇인가 — DevOps와 뭐가 다른가

### 1-1. 왜 생겼나
DevOps로 애플리케이션 배포는 해결했다. 그런데 **머신러닝 모델**을 프로덕션에 올려보니 DevOps만으로 안 되는 게 드러남:

- **코드만이 아니라 데이터와 모델**이 버전 관리 대상
- 학습은 **비결정적** (같은 코드·데이터로도 결과가 조금씩 다름)
- 모델은 **시간이 지나면 성능이 저하** (데이터 드리프트)
- 학습에 **GPU·대용량 데이터·며칠의 시간**이 필요
- 성능 지표가 "pass/fail"이 아니라 **accuracy/F1/latency/cost의 다차원 절충**

→ DevOps의 CI/CD 파이프라인에 **데이터 파이프라인 + 모델 학습 + 실험 관리 + 모델 평가 + 모델 서빙 + 모델 모니터링** 이 추가로 붙음. 이게 MLOps.

### 1-2. 핵심 공식
```
MLOps = DevOps + Data Engineering + ML Engineering
```
- DevOps: 코드 → 배포 자동화
- Data Engineering: 데이터 → 피처/데이터셋 자동화
- ML Engineering: 모델 학습/평가/배포 자동화

**세 개가 수렴하는 지점의 엔지니어 = MLOps**.

### 1-3. DevOps vs MLOps 결정적 차이 4가지

| 축 | DevOps | MLOps |
|---|---|---|
| 배포 산출물 | 실행 가능한 바이너리/컨테이너 | 모델 가중치 파일 + 전처리 코드 + 하이퍼파라미터 + 데이터 스냅샷 |
| 품질 보증 | 단위/통합/E2E 테스트 | 위 + **모델 평가(오프라인) + A/B 테스트(온라인) + 데이터 유효성 검증** |
| 재현성 | 코드만 있으면 재현 | **코드 + 데이터 + 시드 + 환경** 전부 고정해야 재현 |
| 배포 후 | 기능 추가/버그 수정 | **성능 저하 감지 → 재학습 → 재배포** 무한 루프 |

### 1-4. 오해 정리
**"MLOps 엔지니어 = ML 엔지니어"가 아니다.**
- **ML Engineer (MLE)**: 모델을 **만드는 사람**. 알고리즘, 실험, 아키텍처
- **MLOps Engineer**: 모델이 **안정적으로 돌아가게 하는 사람**. 파이프라인, 인프라, 서빙, 모니터링
- **Research Scientist**: 새 알고리즘을 **발견하는 사람**. 논문, SOTA

→ MLOps는 "기반"이고 인접 역할. **모델을 직접 학습시키지 않고도 MLOps를 할 수 있다.** DevOps 출신에게 자연스러운 이유.

---

## 2. MLOps 엔지니어의 실제 업무

### 2-1. 전형적인 하루 (중급 MLOps, Japan Tokyo ML 팀)
```
09:30  Slack + PagerDuty 확인, 야간 추론 latency 알람 리뷰
10:00  스탠드업 (ML팀 + MLOps팀 공동)
10:30  어제 fail 한 학습 job 조사 → GPU OOM → batch size/gradient accumulation 조정 PR
12:00  점심
13:00  ML Engineer A와 1:1 — "새 모델 배포하고 싶은데 vLLM 설정 어떻게?" 문의 대응
14:00  모델 레지스트리(MLflow) 정리, 3개월 안 쓰인 모델 아티팩트 정리
15:30  A/B 테스트 프레임워크에 신규 메트릭(token/s) 추가 PR 리뷰
16:30  데이터 파이프라인 (Airflow DAG) 중 하나가 어제부터 실패 → 디버그
17:30  다음 분기 GPU 클러스터 확장 RFC 문서 작성
18:30  퇴근
```

### 2-2. 업무 비중
| 유형 | 비중 | 구체 예시 |
|---|---|---|
| **모델 서빙 인프라** | 25% | vLLM/Triton 배포, 추론 latency 튜닝, GPU 리소스 관리 |
| **학습 파이프라인** | 20% | Kubeflow/Argo Workflows로 학습 job 자동화, 하이퍼파라미터 튜닝 |
| **데이터/피처 파이프라인** | 15% | Airflow DAG, 피처 스토어(Feast), 데이터 검증(Great Expectations) |
| **실험 관리 / 모델 레지스트리** | 10% | MLflow, Weights & Biases, 모델 버전 관리 |
| **모니터링 / 옵저버빌리티** | 15% | 데이터 드리프트, 모델 성능 저하, Prometheus + 커스텀 메트릭 |
| **ML 팀 지원 / 플랫폼 개발** | 10% | "모델 배포 CLI 도구 만들기", 사내 ML 플랫폼 문서화 |
| **장애 대응 / 온콜** | 5% | 추론 서버 다운, GPU 드라이버 이슈 |

### 2-3. DevOps 업무와의 차이
DevOps의 "K8s 운영 + Terraform + CI/CD" 위에 **모델/데이터/GPU 관리** 3축이 올라감. 시간 비중으로는 DevOps 40%, ML 특화 60%.

---

## 3. 자격 요건 — 기술 스택 체크리스트

### 3-1. 일본 MLOps 공고 기반 핵심 스킬 (Rakuten MDE, PFN, Ubie 등 교차)

| 스킬 | 필수 | 설명 |
|---|---|---|
| **Kubernetes (GPU 워크로드 포함)** | 필수 | NVIDIA Device Plugin, MIG, nodeSelector, GPU autoscaling |
| **Python** | 필수 | 학습 코드/파이프라인/도구 전부 파이썬 |
| **Docker** | 필수 | 모델 컨테이너화 |
| **Terraform** | 필수 | 클러스터 프로비저닝 |
| **CI/CD** | 필수 | GitHub Actions, 모델 배포 파이프라인 |
| **PyTorch 또는 TensorFlow** | 필수 (둘 중 하나) | 프레임워크 레벨 코드 읽기 가능 |
| **MLflow / W&B** | 자주 필요 | 실험 추적 |
| **Airflow / Argo / Kubeflow** | 자주 필요 | 파이프라인 오케스트레이션 |
| **vLLM / Triton / TGI** | **LLM 지향 회사 필수** | Rakuten GPUOD, PFN 필수 |
| **AWS SageMaker or GCP Vertex AI** | 회사별 | 클라우드 ML 서비스 |
| **Feast (피처 스토어)** | 있으면 좋음 | 피처 엔지니어링 일관성 |
| **Ray / Dask** | LLM 학습 지향 | 분산 학습 |
| **CUDA 기본** | 있으면 강력 어필 | GPU 성능 튜닝 |

### 3-2. 레벨별 요구사항 & 일본 연봉

| 레벨 | 경력 | 요구 수준 | 일본 연봉 |
|---|---|---|---|
| Junior | 0~2년 (DevOps 1년+ 有) | 모델 서빙 배포 가능, MLflow 사용 가능 | 600~800만엔 |
| Mid | 2~4년 | 학습 파이프라인 설계, GPU 클러스터 운영, 드리프트 모니터링 구축 | 800~1,200만엔 |
| Senior | 4~7년 | 사내 ML 플랫폼 설계, ML팀 지원 표준 수립 | 1,200~1,800만엔 |
| Staff/Principal | 7년+ | 멀티 리전 ML 인프라, 비용 최적화, 조직 전략 | 1,800만엔+ |

**Rakuten MDE MLOps** 공고 기준: "MLOps 1년+" = Junior 엔트리. DevOps 2년 + 개인 MLOps 포트폴리오로 사정거리 안.

### 3-3. "주니어 MLOps"라 말할 수 있으려면 (체크리스트)

- [ ] K8s에서 GPU Pod 띄우고 `nvidia-smi` 확인 가능
- [ ] vLLM 또는 Triton으로 LLM 추론 서버 배포 가능
- [ ] MLflow에 학습 실험 1개 이상 로깅해봄
- [ ] PyTorch로 간단 모델 학습 및 체크포인트 저장/로드 가능
- [ ] Docker로 모델 + 서빙 코드 패키징 가능
- [ ] Airflow or Argo Workflow로 DAG 1개 작성
- [ ] 모델 성능 저하를 감지할 수 있는 메트릭 2개 이상 설명 가능
- [ ] HuggingFace Hub에서 모델 다운받고 로컬에서 추론 해봄
- [ ] A/B 테스트 기본 개념 (통제군/실험군/통계적 유의성) 설명 가능
- [ ] 데이터 드리프트와 컨셉 드리프트의 차이 설명 가능

→ 7개 이상이면 Junior MLOps 지원 자격, 4~6개면 DevOps→MLOps 전환 준비 중.

---

## 4. 각 기술이 "무엇을 의미하는가"

### 4-1. 모델 레지스트리 (MLflow / W&B)
- **문제**: 학습 실험 100번 돌렸는데 "어떤 조합이 성능 최고였는지" 기억 안 남
- **해결**: 실험마다 하이퍼파라미터/메트릭/아티팩트를 자동 기록. "모델의 Git"
- **핵심 개념**: Experiment, Run, Artifact, Model Registry (Staging/Production 단계)
- **MLOps에서 역할**: 어떤 모델을 배포할지 결정하는 진실의 원천

### 4-2. 피처 스토어 (Feast, Tecton)
- **문제**: 학습에 쓴 피처(예: "최근 7일 구매액")를 추론 시에도 똑같이 계산해야 하는데 코드 중복 + 불일치 발생
- **해결**: 피처를 한 곳에 정의 → 학습/추론 양쪽에서 재사용
- **핵심 개념**: Offline Store (학습용), Online Store (추론용), Feature View
- **언제 필요**: 테이블 기반 ML이 많을 때. LLM 중심 회사(Sakana, ELYZA)는 덜 중요

### 4-3. 파이프라인 오케스트레이션 (Airflow / Argo Workflows / Kubeflow Pipelines)
- **문제**: "데이터 수집 → 전처리 → 학습 → 평가 → 배포"를 매번 수동으로 돌릴 수 없음
- **해결**: DAG(방향 비순환 그래프)로 선언 → 스케줄링/재시도/의존성 자동
- **Airflow**: 범용 데이터 파이프라인 강자. Python 코드로 DAG 작성
- **Argo Workflows**: K8s 네이티브. 모든 step이 Pod. GitOps 친화
- **Kubeflow Pipelines**: Argo 위에 ML 특화 SDK. 하지만 학습 곡선 급함
- **실무 트렌드 (2026)**: Argo + 간단한 SDK로 통일하거나, Dagster/Prefect 같은 현대 대체재 사용

### 4-4. 모델 서빙 (vLLM / Triton / TGI / TorchServe / SageMaker Endpoint)

| 서빙 도구 | 강점 | 언제 쓰나 |
|---|---|---|
| **vLLM** | PagedAttention으로 LLM 추론 throughput 최고 | **LLM 전용. 2026년 현재 사실상 표준** |
| **Triton Inference Server** | NVIDIA 제작, 다중 프레임워크/모델 동시 서빙 | 복합 모델 파이프라인, 엔터프라이즈 |
| **TGI (Text Generation Inference)** | HuggingFace 제작, 간단 | HF 모델 위주, 빠른 POC |
| **TorchServe** | PyTorch 전용 | 레거시, 최근 감소세 |
| **SageMaker Endpoint** | AWS 관리형, 자동스케일 | AWS 올인 조직 |
| **Ray Serve** | 복잡 추론 그래프 | 멀티 스텝 파이프라인 |

### 4-5. 데이터 드리프트 / 컨셉 드리프트
- **데이터 드리프트**: 입력 데이터 분포가 변함 (예: 코로나 후 구매 패턴 변화)
- **컨셉 드리프트**: 입력-출력 관계가 변함 (예: 같은 뉴스에 대한 감정이 시대에 따라 다름)
- **감지 도구**: Evidently AI, Arize, WhyLabs
- **MLOps 역할**: 감지 → 알람 → 재학습 트리거

### 4-6. A/B 테스트 인프라
- **문제**: 새 모델이 정말 더 좋은지 오프라인 메트릭만으론 모름
- **해결**: 사용자의 일부(예: 10%)에게만 새 모델 서빙 → 비즈니스 메트릭(클릭률, 전환율) 비교
- **MLOps 인프라**: 트래픽 분배 (Istio/Linkerd), 메트릭 수집, 통계 검정

### 4-7. GPU 리소스 관리
- **NVIDIA Device Plugin**: K8s가 GPU를 스케줄링 자원으로 인식
- **MIG (Multi-Instance GPU)**: A100/H100을 논리적으로 7조각까지 분할 — 작은 모델 동시 서빙
- **Time-slicing**: 하나의 GPU를 여러 Pod가 시분할 — 저비용 실험
- **Volcano / Kueue**: K8s 기본 스케줄러 위에 ML 특화 배치 스케줄링 (Gang Scheduling)

---

## 5. MLOps 성숙도 (Google의 3단계)

Google이 정의한 업계 표준. **면접에서 자주 물어봄** (특히 Rakuten/PFN).

### Level 0: Manual Process
- 데이터 수집/학습/배포가 **수동**
- 데이터 사이언티스트가 Jupyter에서 모델 훈련 → 운영 엔지니어에게 파일 전달
- **대부분 전통 기업의 출발점**

### Level 1: ML Pipeline Automation
- **학습 파이프라인 자동화** — 새 데이터 들어오면 자동 재학습
- 피처 스토어, 모델 레지스트리 도입
- 배포는 여전히 반수동

### Level 2: Full CI/CD Automation
- **ML CI/CD 파이프라인** — 코드/데이터/모델 전부 자동
- 실험 → 평가 → 승인 → 프로덕션 배포 파이프라인
- 모니터링 → 자동 재학습 트리거
- **Rakuten GPUOD, PFN, Google/Meta 수준**

→ **본인 포지셔닝**: 목표는 Level 2 운영 조직. 지금은 Level 0~1 이해 상태. 이주 후 Level 1→2 경험 축적.

---

## 6. LLMOps — 2026년 특화 영역

LLM이 주류화되면서 전통 MLOps에서 **변형된 과제들**.

### 6-1. LLMOps 고유 이슈
| 이슈 | 전통 MLOps | LLMOps |
|---|---|---|
| 모델 크기 | MB~GB | **10GB~1TB**, 단일 GPU에 못 올림 |
| 학습 비용 | 수 시간~일 | **수주~수개월**, 수십~수백만 달러 |
| 재학습 주기 | 주/월 | **거의 안함**, 파인튜닝/프롬프트 엔지니어링으로 대체 |
| 추론 최적화 | batch inference | **KV 캐시, PagedAttention, Speculative Decoding** |
| 평가 | accuracy/F1 | **LLM-as-a-judge, RAG 평가, 환각 감지** |
| 보안 | 입력 검증 | **프롬프트 인젝션 방어, 출력 필터링, 탈옥 방지** |

### 6-2. 핵심 알고리즘 (Rakuten GPUOD 면접 필독)

- **PagedAttention**: KV 캐시를 OS 페이징처럼 블록 관리 → 외부 단편화 제거, 처리량 3~5배
- **Continuous Batching**: 서로 다른 길이의 요청을 동적으로 배치
- **Speculative Decoding**: 작은 draft 모델이 먼저 추측 → 큰 모델이 검증 → 지연시간 2배 감소
- **Tensor/Pipeline/Data Parallelism**: 거대 모델을 여러 GPU에 쪼개기
- **FlashAttention**: Attention 계산을 GPU SRAM 효율적으로 재설계
- **Quantization (INT8/INT4/FP8)**: 가중치 정밀도 낮춰 메모리/속도 ↑
- **LoRA / QLoRA**: 전체 모델 대신 소수 파라미터만 학습

### 6-3. LLM 운영 스택 (2026 현실적 구성)

```
[Vector DB]       Pinecone / Qdrant / Weaviate / pgvector
       ↓
[Orchestration]   LangChain / LlamaIndex / 직접 구현 (커짐)
       ↓
[Serving]         vLLM / SGLang / TGI / Triton
       ↓
[Infra]           K8s + GPU 노드 + NVIDIA Device Plugin
       ↓
[Monitoring]      Prometheus + LLM 전용 메트릭 (token/s, TTFT, TPOT)
       ↓
[Eval]            Langfuse / Arize / 자체 + LLM-as-judge
       ↓
[Guardrails]      Nvidia NeMo Guardrails / 자체 필터
```

### 6-4. RAG 시스템의 MLOps 포인트
- 문서 업데이트 시 임베딩 재계산 파이프라인
- Vector DB 인덱스 재빌드 스케줄링
- Retrieval 품질 모니터링 (사용자 피드백 루프)
- 생성 품질 평가 (ground truth 있는 질문 세트 자동 평가)

---

## 7. MLOps → LLMOps / MLOps 로드맵 (이주 후 중심)

### 단계 0: DevOps 진입 (6개월 스프린트, 이주 전)
`THE_PLAN.md` 참조. **목표: K8s/Terraform/AWS 기반 + 포트폴리오에 vLLM 미니 데모 1개**.

### 단계 1: 일본 DevOps 현업 축적 (이주 후 0~6개월)
- K8s 프로덕션 운영 실전
- 온콜, 포스트모템
- **퇴근 후 주 4h MLOps 개인 학습**
  - MLflow로 개인 실험 기록 습관화
  - PyTorch 공식 튜토리얼 완주
  - HuggingFace NLP Course 수료

### 단계 2: MLOps 실전 접점 만들기 (이주 후 6~12개월)
- 회사 내 ML 팀과 협업 기회 찾기 (CI/CD 파이프라인 지원 등)
- **사이드 프로젝트**: RAG 챗봇을 K8s에 배포, 직접 운영
- **오픈소스 기여**: vLLM / MLflow / Kubeflow에 작은 PR 1~2개
- Qiita에 MLOps 주제 블로그 월 1건
- **応用情報技術者 취득**

### 단계 3: MLOps 포지션 전환 (이주 후 12~18개월)
- 회사 내 MLOps 팀으로 이동 타진 (내부 이동이 외부 이직보다 빠름)
- **자격증**: GCP Professional ML Engineer or AWS ML Specialty
- 외부 이직 시 타겟: **Rakuten MDE MLOps** (1년+ 경력 요건 충족)

### 단계 4: LLMOps / 분산 추론 영역 (이주 후 18~36개월)
- vLLM/SGLang 프로덕션 운영 경험
- 분산 학습 (FSDP, DeepSpeed) 실전
- **타겟**: **Rakuten GPUOD**, **PFN MN-Core**, **Sakana AI**

### 학습 자료 (이주 후 병행용)
| 자료 | 시점 | 목적 |
|---|---|---|
| [Google ML Engineer 자격증 공식 가이드](https://cloud.google.com/certification/machine-learning-engineer) | 12개월 | 이론 체계화 |
| [Designing Machine Learning Systems - Chip Huyen](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/) | 6개월 | MLOps 바이블 |
| [Machine Learning Engineering - Andriy Burkov](https://www.mlebook.com/) | 9개월 | 실전 감각 |
| [MLOps Community Slack](https://mlops.community/) | 상시 | 최신 동향 |
| [Made With ML](https://madewithml.com/) | 상시 | 무료 엔드투엔드 코스 |
| [Full Stack Deep Learning](https://fullstackdeeplearning.com/) | 12개월 | 실전 |
| [Sebastian Raschka 블로그](https://sebastianraschka.com/blog/) | 상시 | 최신 기술 해설 |
| Andrej Karpathy "Let's build GPT" | 즉시 | Transformer 깊이 이해 |

---

## 8. 이해도 체크 질문 (면접 대비)

### 입문 레벨 (Junior MLOps 면접)
1. MLOps와 DevOps의 차이는?
2. 왜 모델만 배포하는 게 아니라 "모델 + 전처리 코드 + 하이퍼파라미터"를 함께 관리해야 하나?
3. 학습 재현성이 왜 어려운가? 어떻게 확보하나?
4. MLflow가 해결하는 문제는?
5. 데이터 드리프트와 컨셉 드리프트의 차이?
6. K8s에서 GPU Pod를 스케줄링하려면?
7. vLLM이 왜 기존 추론 서버보다 throughput이 높은가?
8. 모델 A/B 테스트를 K8s로 어떻게 구현?
9. 피처 스토어가 필요한 상황과 불필요한 상황?
10. PagedAttention을 OS 페이징으로 설명해보라

### 중급 레벨 (Mid MLOps 면접)
11. 재학습 주기를 어떻게 결정? 트리거 기준은?
12. 학습 파이프라인 실패 시 알람/복구 전략?
13. 모델 배포 시 Shadow Mode vs Canary vs Blue-Green의 차이?
14. LLM 추론 latency 분해: TTFT, TPOT, 전체 latency 최적화 전략?
15. Continuous Batching이 PagedAttention과 어떻게 보완적인가?
16. GPU 비용을 절감하는 방법 5가지?
17. 모델 레지스트리 승격(Staging→Production) 기준을 팀과 어떻게 합의?
18. 분산 학습 Data Parallel vs Tensor Parallel 선택 기준?
19. 프롬프트 인젝션을 프로덕션에서 어떻게 방어?
20. RAG 시스템 품질이 떨어졌다. 원인 후보 5개와 조사 순서?

### LLMOps 특화 (Rakuten GPUOD 면접)
21. vLLM의 block_manager는 무엇을 관리하고, block size를 키우면 장단점?
22. Speculative Decoding이 왜 효과적이고, 언제 비효율적?
23. KV 캐시를 여러 요청이 공유하는 시나리오 2가지? (parallel sampling, prefix caching)
24. H100 SXM의 메모리 대역폭이 왜 중요한가? A100 대비 뭐가 다른가?
25. FSDP ZeRO-3에서 gradient와 parameter가 어떻게 샤딩되는지 설명

---

## 9. MLOps 지원 가능 일본 회사

### Tier S (최상위 / 경력 3년+ 필요)
| 회사 | 포지션 | 특징 |
|---|---|---|
| **Rakuten GPUOD** | Distributed Training & Inference Optimization | vLLM/SGLang/분산추론, 영어 공용 |
| **Preferred Networks (PFN)** | MN-Core SW / Foundation Models | 자체 AI 칩 + LLM |
| **Sakana AI** | Research / ML Engineer | ex-Google Brain 창업 |

### Tier A (엔트리 ~ 미드)
| 회사 | 포지션 | 매칭 |
|---|---|---|
| **Rakuten MDE** | MLOps Engineer | **MLOps 1년+** = 이주 후 12개월차에 사정거리 |
| **Ubie** | ML Platform Engineer | 헬스케어 AI, GCP+K8s, 글로벌팀 영어 OK |
| **ELYZA (KDDI)** | LLM / MLOps Engineer | 일본어 LLM, 일본어 필수 |
| **AIRoA** | MLOps Engineer | 로보틱스 + ML |

### Tier B (엔트리)
| 회사 | 포지션 | 매칭 |
|---|---|---|
| **Mercari AI Platform** | ML Engineer / Platform | 영어 공용 |
| **LayerX AI** | ML Engineer | 문서 AI, 성장 중 |
| **Autify** | MLOps / Platform | QA AI, 영어 공용 |
| **SmartNews** | ML Platform | 뉴스 추천, 영어 공용 |
| **DeepX** | ML Engineer | 건설 AI |

### Tier R (연구 성향)
- Rakuten Institute of Technology (RIT)
- Sony AI
- LY Corporation Labs
- CyberAgent AI Lab

---

## 10. 현 포지션(6개월 스프린트)에서 MLOps 대비로 꼭 할 것

이주 전 DevOps 취업 스프린트 기간 동안 **싸게 넣을 수 있는 MLOps 씨앗**:

1. **포트폴리오에 vLLM 마이크로서비스 1개 포함** — 이미 THE_PLAN 반영됨
2. **PagedAttention 블로그 1건 (일본어)** — MLOps 관심의 가시적 증거
3. **MLflow로 개인 실험 1~2개 기록** — 5시간 투자로 "MLflow 안다" 가능
4. **HuggingFace Hub에 모델 1개 업로드** — 소형 파인튜닝 결과, 프로필 크레딧
5. **Kubeflow 개요 숙지** — 면접에서 "Kubeflow 공식 아키텍처 기준으론..." 한 마디 가능
6. **LLMOps 용어 10개 암기**: TTFT, TPOT, PagedAttention, Continuous Batching, KV Cache, FSDP, LoRA, RAG, Vector DB, Speculative Decoding

---

## 11. 핵심 메시지 요약

1. **MLOps는 DevOps + Data + ML**. DevOps 기반이 탄탄해야 MLOps가 쉽다
2. **모델은 코드가 아니다**: 데이터·시드·환경·하이퍼파라미터 전체가 배포 산출물
3. **LLMOps는 MLOps의 하위 집합이 아니라 변종**. 비용/규모가 달라서 재학습 주기, 서빙 최적화, 보안 전부 다름
4. **2026년 현장 표준 스택**: K8s + vLLM + MLflow + Argo/Airflow + Prometheus + Vector DB
5. **DevOps 엔지니어의 가장 빠른 MLOps 전환 루트**: 사내 ML팀과 협업 → 내부 이동. 외부 이직은 실전 1년 후
6. **PagedAttention은 OS 페이징**. 그 이상도 이하도 아님. 이 프레임을 가지면 LLM 서빙 80% 설명 가능
7. **포트폴리오 1개 (vLLM on EKS) + 블로그 1건 (PagedAttention)** 이면 주니어 MLOps 서류 통과 가능. 나머지는 면접에서 승부

---

## 12. 이 문서의 운영

- **이주 후 3개월마다 재독**
- Rakuten MDE 등 타겟 공고 요건 변경 시 본 문서 3~4장 반영 수정
- `devops-deep-dive.md` 와 상호 참조. 한쪽 업데이트 시 다른 쪽 정합성 확인
