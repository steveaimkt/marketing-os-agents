---
name: 실습-6-4-3media-integrated
description: |
  Part 6 클립 6-4 (3매체 통합 리포터) 실습 시연 스킬. 사용자 한 줄 명령 →
  ① 소개 (하는 일 + 연결 소스) → ② 실행 (작동 구조 + 데이터 준비 + 실제 실행) →
  ③ 활용 (내 업무에 적용하는 방법).
  흐름 : ① 소개 ② 실행 ③ 활용. 자동 실행 금지. 단계마다 답 받고 다음.
  입력 우선순위 : 선행 6-1~6-3 의 실제 산출물(outputs/{날짜}/…)을 먼저 쓰고,
  없으면 04 내장 픽스처로 폴백해 단독 촬영도 가능하다.
  에이전트가 에이전트 3개를 호출하는 상위 오케스트레이션 구조가 학습 핵심.

  자동 호출 트리거:
  - **"6-4 실습 시작"** ⭐ 주요 트리거
  - "통합 리포트 실습" / "3매체 리포트 실습 시작하자"
  - "3media 실습" / "매체 통합 시연"

  동작: 한 줄 → 3 단계 인터랙티브 → outputs/{날짜}/3media-report-{날짜}.html
  (비교표 + 인사이트 + 재배분 제안) + Notion 아카이브 → 다음 클립 (6-5) 제안.
---

# Part 6 / 6-4 · 3매체 통합 리포터 실습 : 소개 → 실행 → 활용

> Meta·Google·Naver 분석 결과를 모아 **한 장의 통합 리포트와 예산 재배분 제안**을 만드는 에이전트를 가동한다.
> 핵심 학습 목표 : ① 에이전트가 에이전트 3개를 호출 (상위 오케스트레이션 맛보기) ② 매체 간 동일 잣대 비교 ③ 제안과 실행의 분리.
> ⛔ 자동 실행 금지. 단계마다 사용자 답을 받은 뒤에만 다음으로.

## 진행 흐름 (3 단계)

```
1단계  소개   하는 일 + 연결 소스 + 핵심 포인트          ⏸
2단계  실행   사전 점검 → 작동 구조 → 데이터 준비 → 실제 실행  ⏸
3단계  활용   내 업무 적용법 + 산출물 + 다음 클립          ⏸
```

---

## 1단계 · 소개

```
🧩 3매체 통합 리포터가 하는 일

  "매체별 리포트 3개를 사람 머릿속에서 합치지 말 것. 동일 잣대 비교표 1장으로."

  · Before : Meta 화면 + Google 화면 + 네이버 화면 번갈아 보며 감으로 예산 판단
  · After  : 통합 HTML 1장 : 매체별 ROAS·CPA 나란히 + 재배분 제안까지 = 3분
```

🔌 연결 소스 (실제 의존만)

```
3media-integrated-reporter
  ├─ Agent(meta-ads-analyzer)      ← Meta 결과 수집
  ├─ Agent(google-ads-analyzer)    ← Google 결과 수집
  ├─ Agent(naver-ads-analyzer)     ← Naver 결과 수집
  ├─ Skill(html-report-template)   ← 통합 HTML 디자인
  └─ Notion                        ← 아카이브 1행
```

💡 핵심 포인트 : 이 에이전트는 **에이전트가 에이전트 3개를 호출하는 상위 오케스트레이션**이다.
  하위 3개의 출력이 이 에이전트의 입력이 된다 (Part 10 오케스트레이터 예고편).
  단, 6-4 는 **고정된 3개 호출** · Part 10 은 **자연어 라우팅** 이라는 점이 다르다.

📐 **스킬? 에이전트?** → 하위 에이전트 3개 호출 + 산출(HTML·Notion)이 있으니 🤖 **에이전트(오케스트레이션형)**. 리포트는 html-report-template **스킬** 공유. = Part 10 오케스트레이터의 축소판.

⏸ "다음" 확인 받고 2단계로.

---

## 2단계 · 실행

### 2-0 사전 점검

```bash
# 리포트 템플릿 · webhook
test -f "skills/html-report-template/SKILL.md" && echo "리포트 템플릿 ✅"
test -f "discord-bot/webhook-config.json" && echo "webhook ✅"

# 선행 6-1~6-3 라이브 산출물 탐색 (있으면 이것을 통합 기준으로 사용)
ls outputs/*/meta-roas-*.html 2>/dev/null && echo "6-1 Meta 산출물 ✅"
ls outputs/*/google-ads-analyzer/google-ads-keyword-*.html 2>/dev/null && echo "6-2 Google 산출물 ✅"
ls outputs/*/naver-ads-analyzer/*.html 2>/dev/null && echo "6-3 Naver 산출물 ✅"
```

```
🔧 6-4 의존 항목 점검 결과   (입력 우선순위 : 라이브 산출물 → 없으면 픽스처)

  | # | 항목 | 용도 | 상태 | 입력 경로 (우선 → 폴백) |
  |---|---|---|---|---|
  | ① | 6-1 Meta 결과    | 통합 입력 | {✅ 산출물 / 픽스처} | outputs/{날짜}/meta-roas-{날짜}.html → sample-data/meta-ads-performance.json |
  | ② | 6-2 Google 결과  | 통합 입력 | {✅ 산출물 / 픽스처} | outputs/{날짜}/google-ads-analyzer/google-ads-keyword-{날짜}.html → sample-data/google-ads-performance.json |
  | ③ | 6-3 Naver 결과   | 통합 입력 | {✅ 산출물 / 픽스처} | outputs/{날짜}/naver-ads-analyzer/ → sample-data/naver-ads-performance.json |
  | ④ | html-report-template | 리포트 디자인 | {✅ / ❌} | 0분 |
  | ⑤ | Notion · webhook | 아카이브 + 알림 | {✅ / ❌} | 1~10분 |

  선행 6-1~6-3 산출물이 있으면 그 결과를 그대로 통합 입력으로 사용한다 (사용자 기준).
  6-1~6-3 을 안 했거나 산출물이 없으면 내장 픽스처 3종으로 폴백 → 단독 촬영 가능.
  실전 모드 : 6-1~6-3 에이전트를 병렬 호출 (& + wait) 해 라이브 결과로 통합.
```

### 2-1 작동 구조

```
🔄 에이전트 워크플로
  [3매체 분석 결과]
    → (실전) meta·google·naver 분석 에이전트 3개를 병렬 실행 후 수집
    → 섹션 1 : 매체 비교표 (지출 · ROAS · CPA · CTR 동일 잣대)
    → 섹션 2 : 인사이트 5줄 (왜 A 매체가 B 보다 효율적인가)
    → 섹션 3 : 예산 재배분 제안 (현재 배분 vs 효율 기준 배분)
    → HTML 리포트 + Notion 아카이브

🛡 제안과 실행의 분리 : 재배분은 "제안"까지만.
   예산 변경은 사용자 승인 영역 (안전 원칙).
```

`agents/part6-ads/3media-integrated-reporter.md` 에서 새로 볼 부분:
  ① tools 에 다른 에이전트 3개 : 에이전트의 입력이 에이전트의 출력
  ② 병렬 실행 패턴 : 순차가 아니라 동시에 (& + wait) · 시간 1/3
  ③ 재배분 "제안" 형식 : 현재 vs 제안 비율 + 근거 + 예상 효과, 실행 버튼은 없음

### 2-2 데이터 준비 (3매체 입력 — 라이브 산출물 우선)

입력 우선순위 : **① 선행 6-1~6-3 의 실제 산출물 → ② 04 내장 픽스처(폴백)**

```
  · 6-1 Meta   : outputs/{날짜}/meta-roas-{날짜}.html
                 (없으면 sample-data/meta-ads-performance.json)
  · 6-2 Google : outputs/{날짜}/google-ads-analyzer/google-ads-keyword-{날짜}.html
                 (없으면 sample-data/google-ads-performance.json)
  · 6-3 Naver  : outputs/{날짜}/naver-ads-analyzer/
                 (없으면 sample-data/naver-ads-performance.json)
```

로드 후 매체별 핵심 숫자 미리보기:

```
📥 3매체 결과 (7일 · 동일 기간 2026-06-04 ~ 06-10)
  · Meta   : 지출 295만 · 매출 720만 · 전환 챌린지 ROAS 3.80 (리치 0.43 부진)
  · Google : 토너 키워드군 전환가치 약 590만 · 브랜드 강세 · 품질점수 경고 2건
  · Naver  : 지출 291만 · 합산 ROAS 1.54 (브랜드 7.41 / 일반 0.71 분리 완료)
```

### 2-3 실제 실행 (★ 고도화 사양 — `report-spec.md` 준수)

> 표준 형식은 `report-spec.md`, 표준 템플릿은 `sample-output/3media-report-upgraded.html`.
> 리포트는 "비교"에서 멈추지 말고 **"어디서 빼서 어디에 넣어라"**까지 답한다.

```
▶ 워크플로 단계별 실행:

  1. 3매체 결과 수집 (선행 6-1~6-3 산출물 우선 → 없으면 픽스처 → 실전은 병렬 호출)
       + 세그먼트 단위 분해 (Meta=광고세트 / Google=브랜드·일반·저품질 / Naver=브랜드·일반)
  2. 매체 3색 고정 : Meta #1877F2 · Google #F59E0B · Naver #03C75A (초록 충돌 금지)
  3. 섹션 1 다지표 매트릭스 (9지표)         → ROAS·CPC·CAC·CTR·CVR·CPM·AOV + 행별 최고/최저
  4. 예산 최적화 코어 4종 (인라인 SVG):
       ② 효율–지출 4분면 맵 (STAR/SCALE/CUT/PRUNE)
       ③ 효율 프론티어 (BEP 미만 예산 % 표시)
       ④ 재배분 워터폴 (매출 증분 원 단위 + ROAS 델타)
       ⑤ 고의도 vs 저의도 3매체 그룹막대
  5. 인사이트 4~5줄 + 재배분 제안(매체 % + 세그 단위 지시) + 액션 체크박스
       매체 간 ROAS 직접 비교 주의 주석(어트리뷰션) · 재배분은 "제안"까지만
  6. HTML 리포트 생성                       → outputs/{날짜}/3media-report-{날짜}.html
  7. Notion 아카이브 + Discord 요약
```

(간단 시연만 원하면 코어 4종 중 ②④ 로 축약 가능. 풀 대시보드 요청 시 보조 3종 추가.)

⏸ 리포트 확인 후 3단계로.

---

## 3단계 · 활용 — 지금, 내 업무로

### 적용 게이트 (능동 질문 ⏸)

```
🚀 그럼, 지금부터 내 업무에 적용해볼까요?

   ① 어떤 브랜드/업종인가요?
   ② 통합할 매체는?                     (Meta · Google · 네이버 중 보유한 것)
   ③ 예산 재배분 제안까지 볼까요?       (예 / 비교표만)
```

→ 답을 받으면 : 매체 비교표 + 통합 인사이트 + (선택) 재배분 제안 HTML 1장.
→ "건너뛰기" 시 아래 정착 가이드만.

### 오래 쓰는 법 (적용 후 정착)

🎯 내 업무에 적용하는 방법

```
1. 매체 추가/교체 : tools 목록에 새 매체 분석 에이전트만 추가하면 N매체 통합으로 확장
2. 주간 자동 통합 : cron 으로 매주 월요일 자동 생성 → Discord 발송 (Part 10)
3. 재배분 근거화 : "감으로 예산 증액" 대신 동일 잣대 비교표를 회의 자료로 사용
4. 오케스트레이션 패턴 학습 : 이 구조가 Part 10 메인 오케스트레이터의 축소판
```

📊 산출물

```
   · 로컬   : outputs/{날짜}/3media-report-{날짜}.html
             (다지표 매트릭스 9지표 + 코어 4시각화 + 인사이트 + 재배분 · report-spec.md 준수)
   · Notion : 아카이브 1행
   · Discord: 요약 embed

✅ 체크리스트:
   [ ] 에이전트가 에이전트 3개를 호출하는 구조를 설명할 수 있음
   [ ] 매체 간 ROAS 직접 비교의 함정 (기여 모델) 인지
   [ ] 재배분이 제안에서 멈추는 이유 (실행은 사용자 승인 영역)
```

🔁 다음 클립

```
   A. "6-5 실습 시작" : 광고 성과 임계값 감시 (시간당 자동 체크)
   B. 실전 모드 : 6-1~6-3 라이브 병렬 실행으로 재생성
   C. 주간 자동 통합 리포트 cron 등록 (Part 10)
```
