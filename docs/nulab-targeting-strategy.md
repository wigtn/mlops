# Nulab 공략 전략 — 공고 없어도 들어가는 법

> Nulab 공식 채용 페이지 확인 결과: **현재 공식 공고 0건**.
> 단, **카주얼 면담 창구 + 리퍼럴 창구는 항상 열려있음** → 공고 등록 전 선점 가능.
> 본 문서는 "공고 없는 회사에 눈에 띄게 해서 뽑히는 법"을 Nulab 맞춤으로 설계.

---

## 1. 현재 채용 상황 (확인일: 2026-04-15)

### 공식 공고
- **현재 공고**: **0건** ("恐れ入りますが、現在募集中のポジションはありません")
- 출처: https://careers.nulab.com/entry/

### 실제로는 열려있는 2개 창구
| 창구 | URL | 용도 |
|---|---|---|
| **カジュアル面談 (Casual Conversation)** | https://herp.careers/v1/nulab/uPb8iFlFjGZo | 현직자와 30분 대화. 지원 아님. **1차 관문** |
| **リファラル採用窓口 (Referral)** | https://herp.careers/v1/nulab/E8bjhtcGUXtx | 재직자 추천 전형 전용 |

### 채용 중인 부서 (공고 없어도 관심 수용)
- **Service Development (サービス開発部)** — 제품 개발
- **Reliability Engineering部** ★ ← **본인 타겟. SRE/인프라 조직**
- Product Management
- Business Growth
- Customer Communication
- RevOps
- Corporate

→ **Reliability Engineering部 카주얼 면담 신청 = 정답**

---

## 2. Nulab이 원하는 인재상 "Nuice Ways" 분석

Nulab 채용 폴리시에 명시된 3개 가치. **면접/카주얼 면담/자기소개 전체에 이 3축으로 일관된 스토리 구성 필수**.

### 2-1. **Try First** — 도전/학습 지향
원문: "常識や現状ボーダーにとらわれずに挑戦し、向上しようとする"

**의미**: 관행/경계에 얽매이지 않고 시도하고 향상시킴. Bottom-up 아이디어 존중.

**내가 어필할 각도**:
- 한국 IT 회사에서 풀스택(잡부) → **DevOps/MLOps 방향을 스스로 설계하고 학습** 중
- **일본 이주 + 커리어 전환** 자체가 "現状ボーダー"를 넘는 행동
- 6개월 스프린트로 포트폴리오 1개 완성 (Terraform+EKS+vLLM...) → **"시도해서 만들었다"**의 증거
- PagedAttention을 OS 페이징에서 이해하려 했던 접근 = 자발적 깊이 추구

### 2-2. **Love Differences** — 다양성 존중
원문: "オープンマインドを持ってお互いを尊重"

**의미**: 백그라운드/기술/문화/선호 다양성 존중. 분산 국제 팀 전제.

**내가 어필할 각도**:
- 한국인 + 일본인 배우자 + 일본 이주 = **다문화 가정 = 살아있는 증거**
- 한국/일본 IT 문화 모두 경험 → **문화 번역자** 포지셔닝
- Nulab의 NY/암스테르담 오피스와 협업 상상하면 강력한 자산
- Backlog가 180개국 사용자 대상 → 다국적 사용자 이해도 자연스럽게 연결

### 2-3. **Goal Oriented** — 본질 유지 + 투명한 목표 공유
원문: "本質を見失わないよう、オープンな場でゴールを議論し、共有"

**의미**: 목표 투명성, 심리적 안전성, 본질 유지.

**내가 어필할 각도**:
- 현 회사에서 "풀스택 잡부"로 일하면서도 **본질적 커리어 방향(MLOps)을 정의하고 계획한 것**
- 이 docs 레포 자체 = 목표를 문서화하고 단계화한 투명한 증거물 → **GitHub 공개 강력 추천**
- 과거 프로젝트에서 "왜 이걸 하는가"를 팀과 공유한 경험 서사화

---

## 3. 채용 폴리시의 숨은 기회

Nulab 폴리시의 **"비평가 항목"** 직접 명시:
> 学歴 / 年齢 / 性別 / 容姿 / 家族構成 / **国籍** / 思想・信条

→ **국적이 평가 대상 아님** 을 공식 선언. 한국인 + 배우자 비자 = **정치적으로 100% 청정**. 대부분 일본 회사는 외국인 채용에 리스크 감각 있음. Nulab은 명시적으로 중립 = 진입 장벽 1개 소멸.

또한:
> 小規模組織のため一人の採用がカルチャーに大きく影響する

→ **컬처 핏 엄격**. 기술만 어필하면 탈락. **"Nuice Ways" 스토리를 기술 어필 위에 반드시 얹어야 함**.

---

## 4. 12단계 공략 플랜 (공고 없는 상태에서 들어가는 로드맵)

### 🔵 Step 1: 정찰 (Week 0, 즉시)
1. **Nulab 제품 전부 실제 사용**:
   - Backlog 무료 트라이얼 계정 → 한 달 사용하며 UX 관찰
   - Cacoo로 본인 포트폴리오 아키텍처 다이어그램 그리기 → **이력서/블로그에 Cacoo 임베드**
   - Nulab Pass 개요 학습
   - **면담에서 "실제로 써봤습니다, X 기능이 Y 점에서 좋았습니다" = 결정적 차별화**
2. **Nulab 엔지니어링 블로그 아카이브 정독**:
   - https://nulab.com/blog/ (영어)
   - https://nulab.com/ja/blog/ (일본어)
   - 특히 **Reliability Engineering 관련 포스트 3건** 뽑아서 노트
3. **GitHub @nulab 스타 리포 TOP 5 확인** → 기술 스택 파악, 가능하면 **아주 작은 PR/이슈** 1건
4. **LinkedIn에서 현 Nulab 엔지니어 10명 식별** (후쿠오카/도쿄/NY/암스테르담)

### 🔵 Step 2: 포트폴리오를 "Nulab 맞춤"으로 만든다 (Week 1~16)
기존 6개월 플랜의 포트폴리오 `infra-platform-demo`에 **Nulab 특화 시그널 주입**:

| 기존 | Nulab 맞춤 추가 |
|---|---|
| FastAPI 단일 앱 | "소규모 협업 팀을 위한 프로젝트 관리 API" 라는 테마 — **Backlog 사용자 관점에서 설계** |
| README 영문 | 영문 + 일문 + **아키텍처 다이어그램은 Cacoo로 그림** |
| 블로그 |  **"Backlog APIをTerraformで管理してみた"** 같은 Nulab 생태계 연계 블로그 1건 |
| 일반 K8s 예제 | **Backlog Git Webhook → ArgoCD 트리거** 같은 Nulab 제품 실제 활용 |

→ 면담 자리에서 "저희 제품으로 뭐 만들어 봤어요" = **기억되는 지원자**

### 🔵 Step 3: 일본어/영어 자기소개 Nulab 맞춤 스크립트 (Week 10~16)

#### 영어 버전 (90초)
```
Hi, I'm Jinmo. I'm a full-stack engineer based in Seoul, transitioning
into platform/SRE work. I'm moving to Japan later this year — my wife
is Japanese — and Nulab specifically caught my attention because of
how you've built a 20-year global SaaS business with just ~150 people,
from Fukuoka. That scale-to-complexity ratio is exactly where I want
to work.

I've been building a demo: Terraform-provisioned EKS running a small
collaboration API, with GitOps via ArgoCD and full observability.
I modeled the architecture in Cacoo — happy to share.

I'm especially curious about the Reliability Engineering team's
approach to Backlog's global multi-region footprint.
```

#### 일본어 버전 (90초)
```
ジンモと申します。韓国・ソウルでフルスタック開発をしていますが、
プラットフォーム/SRE方向へキャリアを転換中です。年内に日本移住予定で、
妻が日本人なのでビザの心配はありません。

Nulabを選んだのは、150名規模で20年にわたりグローバルSaaSを運営している
という希少な実績に強く惹かれたからです。個人的にBacklogを1ヶ月使い、
Cacooでポートフォリオのアーキテクチャ図を作りました。

Terraform+EKS+ArgoCDでコラボレーションAPIを構築するデモを作っており、
Reliability Engineering部がBacklogのマルチリージョン運用をどう設計
されているか、ぜひお話を伺いたいです。
```

**Nuice Ways 3축 암묵 반영 체크**:
- Try First → 직접 써봤다, Cacoo로 그렸다, 데모 만들었다
- Love Differences → 다문화 가정, 한국/일본 커리어
- Goal Oriented → "MLOps 방향으로 커리어 전환 중" 본질 명시

### 🔵 Step 4: 카주얼 면담 신청 (Week 17)
1. 링크: https://herp.careers/v1/nulab/uPb8iFlFjGZo
2. 希望 팀: **Reliability Engineering部**
3. 希望 언어: **일본어 + 영어 병행 가능**
4. 메시지 본문 (한국어 번역 제공):

```
【일본어 원문】
Nulabのカジュアル面談に応募させていただきます。

韓国ソウル在住のフルスタックエンジニアで、2026年X月頃に配偶者ビザで
東京または福岡への移住を予定しています。

Nulabに興味を持った理由:
- 福岡発で20年以上、少人数でグローバルSaaSを運営されている点
- 採用ポリシーの国籍非評価・多様性重視の姿勢
- Reliability Engineering部がBacklog/Cacooのようなグローバル
  サービスを支えるスケール

自主学習として Terraform + AWS EKS + ArgoCD によるインフラ
ポートフォリオを構築中で、アーキテクチャ図はCacooで作成しました。
GitHub: https://github.com/[...]/infra-platform-demo

将来的にはMLOps領域に進みたく、その布石としてプラットフォーム/SRE
の深い運用経験を積みたいと考えております。

Reliability Engineering部の方とお話しできれば幸いです。
日本語・英語どちらでも対応可能です。
```

### 🔵 Step 5: 리퍼럴 루트 병행 (Week 17~20)
1. LinkedIn에서 **Nulab Reliability Engineering / SRE / DevOps** 직함 검색
2. 후보자:
   - 후쿠오카/도쿄 거주 일본인 엔지니어
   - NY/암스테르담 거주 외국인 엔지니어 (영어 편함)
   - 특히 **한국인/한국계 Nulaber가 있으면 최우선**
3. 메시지 템플릿 (영어):

```
Hi [Name], I've been following Nulab's engineering blog and
enjoyed your [specific post / project]. I'm a full-stack engineer
transitioning into SRE/platform work, and planning to relocate to
Japan later this year. Would you be open to a 20-minute chat
about your experience on the Reliability Engineering team?
No pressure — I'm genuinely trying to understand the team culture
before considering applying.
```

**핵심 규칙**:
- 첫 메시지에서 **추천 요청 금지** (무례)
- 3번 이상 대화 후 자연스럽게 "혹시 careers 페이지에 공고 뜨면 알려주실 수 있나요" 로 서서히 접근
- 리퍼럴은 결과물, 요청이 아님

### 🔵 Step 6: 카주얼 면담 실전 (Week 18~20)
- **30분 세팅, 본인은 25분 들음, 5분 질문**
- 필수 질문:
  1. Reliability Engineering 팀 현재 가장 큰 챌린지?
  2. Backlog 멀티 리전 운영에서 K8s가 어디까지 쓰이나?
  3. 최근 1년 팀에 사람 늘었나? (= 채용 의향 탐색)
  4. 팀원의 하루는? (컬처 파악)
  5. 새로 들어온 엔지니어가 제일 잘한다고 느끼는 스킬?
- **마지막 1분**: "혹시 공고 오픈 되면 어떻게 알 수 있을까요?" → 자연스럽게 follow-up 약속
- 면담 후 24시간 안에 **영어 + 일본어 병기 감사 메시지** 송부

### 🔵 Step 7: 정기 존재감 유지 (Week 18~24)
공고 없는 회사를 기다리려면 **잊혀지지 않는 게 핵심**:
1. Qiita에 **Nulab 제품 관련 기술 블로그 1건** 공개
   - 예: "Backlog Webhook と Terraform Cloud で PR 自動化してみた"
   - Twitter/X로 해당 블로그를 공유하면서 **@nulabinc** 멘션
2. LinkedIn에서 Nulab 블로그 포스트에 **사려깊은 코멘트** (월 2건)
3. Cacoo/Backlog 업데이트 나올 때마다 실제 써보고 블로그 달기
4. 면담에서 만난 엔지니어에게 2개월 주기 근황 업데이트 ("블로그 하나 더 썼어요" 수준)

### 🔵 Step 8: 공고 오픈 시 즉시 지원 (Week 25 이후, 공고 뜨면)
공고 등록 **24시간 내 지원** — 내부적으로 이미 카주얼 면담/리퍼럴 네트워크 구축됐으므로 서류 통과율 압도적.

### 🔵 Step 9~12: 대체 시나리오
**24주 안에 Nulab 공고가 안 뜨면**:
- Step 9: Autify (도쿄, 영어 공용) 정식 지원
- Step 10: Ubie (도쿄, 헬스케어 AI) 정식 지원
- Step 11: Cybozu (오사카/리모트, K8s 기술 매칭)
- Step 12: Nulab은 **입사 후 2~3년차 경력직 재도전** (더 강력한 카드로)

---

## 5. Nulab 면접 시 예상 질문 Top 10

1. "どうして日本で働きたいですか？" (왜 일본?) — 배우자 + 커리어 진정성 있게
2. "なぜNulabですか？他のSaaS会社ではなく？" (왜 Nulab?) — 20년 안정 + 150명 글로벌 + 후쿠오카 모델
3. "Backlog/Cacooの使用感はどうでしたか？" — **실제로 써봐야 답 가능**
4. "チームで意見が割れた時はどう動きますか？" — Goal Oriented (본질 논의 + 심리적 안전성)
5. "最近挑戦したことは？" — Try First
6. "文化が違う相手と仕事をした経験は？" — Love Differences (다문화 가정)
7. "5年後のキャリアイメージは？" — MLOps 방향 진솔하게 (Nulab에서 Platform → ML 방향 성장 가능성 언급)
8. "Kubernetesで一番ハマったトラブルは？" — 기술 디테일
9. "なぜフルスタックからSRE/Platformへ？" — 본질 탐구 서사
10. "逆質問ありますか？" — 위 Step 6의 5개 질문 재활용

---

## 6. 체크리스트 (지원 전 자가 진단)

- [ ] Backlog 1개월 이상 사용함
- [ ] Cacoo로 포트폴리오 다이어그램 1장 그림
- [ ] Nulab 블로그 포스트 10건 이상 읽음 (Reliability Engineering 주제 3건 포함)
- [ ] 포트폴리오 리포에 Cacoo 다이어그램 임베드
- [ ] Nulab 제품 활용 블로그 1건 Qiita 공개
- [ ] LinkedIn에서 Nulab 엔지니어 5명 이상 connect
- [ ] 자기소개 일본어/영어 각 90초 버전 암기
- [ ] Nuice Ways 3가지를 내 이야기로 3분 설명 가능
- [ ] 카주얼 면담 메시지 템플릿 준비
- [ ] 리퍼럴 요청 타이밍 전략 수립

---

## 7. 본 문서 운영

- **월 1회 Nulab careers 재확인**: https://careers.nulab.com/entry/
- **공고 뜨는 순간 본 문서 Step 4~5 재실행**
- 다른 회사(Autify/Ubie 등)는 `6month-sprint-plan-v2.md` 와 `regional-expansion.md` 대로 병렬 진행
- Nulab은 **병렬 트랙의 최우선 타겟**, 단 공고 의존도 있으므로 백업 라인 절대 포기 금지
