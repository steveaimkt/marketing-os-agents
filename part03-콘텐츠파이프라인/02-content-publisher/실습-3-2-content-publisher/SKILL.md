---
name: 실습-3-2-content-publisher
description: |
  Part 3 클립 3-2 (콘텐츠 자동 업로드 에이전트) 실습 시연 스킬. 사용자 한 줄 명령 →
  ① 소개 (에이전트 기능 + 연결된 소스 안내) →
  ② 실행 (작동 워크플로 구조 + 실제 실행: 채널별 변형 → ⏸승인 → Buffer 큐잉 → Notion 동기화) →
  ③ 활용 (내 업무에 적용하는 방법).
  자동 실행 금지. 단계마다 사용자 답을 받은 뒤 다음으로.
  샘플 데이터 모드 기본 (결로아 Draft 3건) · 실데이터 모드 선택 가능.

  자동 호출 트리거:
  - **"3-2 실습 시작"** ⭐ 주요 트리거
  - "콘텐츠 퍼블리셔 실습" / "콘텐츠 자동 업로드 실습"
  - "content-publisher 실습" / "Buffer 큐잉 실습"
  - "SNS 자동 업로드 시연"

  동작: 한 줄 → 3 단계 인터랙티브 → Draft 3건이 채널별 변형되어 Buffer 큐에 예약 +
  Notion 상태 Draft → Scheduled + Discord 큐잉 확인 → 다음 클립 (3-3) 제안.
---

# Part 3 / 3-2 · 콘텐츠 자동 업로드 에이전트 실습 : 소개부터 큐잉까지

> 노션 콘텐츠 캘린더의 Draft 를 **5개 SNS 채널에 동시 변형·예약**한다.
> 1주일치 콘텐츠 큐잉이 명령 1줄. 핵심 학습 목표 : ① 채널별 자동 변형 ② 항목별 승인 게이트 ③ 중복 방지.
> ⛔ 자동 실행 금지. 단계마다 사용자 답을 받은 뒤에만 다음으로.

## 진행 흐름 (3 단계)

```
1) 소개   이 에이전트가 뭘 하는지 + 연결된 소스          ⏸ 다음
2) 실행   작동 구조 보여주고 실제 실행 (승인 → 큐잉)       ⏸ 승인/선택
3) 활용   내 업무에 어떻게 적용할지 안내                  ⏸ 선택
```

---

## 1단계 · 소개

**하는 일 (한 줄)** : 같은 원본 1개 → 채널별 맞춤 변형 N개, 사람은 승인만.

```
⏱ Before vs After
  · Before : 콘텐츠 1건당 채널별 수동 변형 5회 × 10분 + 채널별 예약 5회 × 3분 = 약 65분/건
  · After  : Draft 상태로 두면 명령 1줄에 변형·큐잉 완료 = 약 2분/건 (30배 단축)
```

🔌 **연결된 소스** (이 실습이 의존하는 것만)

```
content-publisher (에이전트)
├─ MCP   mcp__claude_ai_Notion__*   콘텐츠 캘린더 읽기·쓰기 (Draft → Scheduled)
├─ MCP   mcp__buffer__*             SNS 채널 예약 큐잉 (IG·FB·X·LinkedIn·TikTok)
├─ Skill brand-voice                채널별 변형 시 브랜드 톤 적용
└─ 산출  Discord webhook            승인 요청 + 큐잉 확인 embed
```

🛡 **핵심 안전 원칙 3가지**
- 반드시 사용자 승인 후 큐잉 (자동 큐잉 절대 금지)
- 7일 이내 동일 내용 발행 이력 → 중복 경고
- 이미지 URL 없으면 발행 보류

📐 **이 업무는 스킬일까 에이전트일까?** (5문 판별)

```
  Q1 외부 도구(MCP) 필요?   → Notion·Buffer ✅
  Q2 트리거로 스스로 도나?  → /publish-this-week ✅
  Q3 산출물이 밖으로 나가나? → Buffer·Notion·Discord ✅
  Q4 순수 변환(입력만 바뀜)? → ❌
  ─────────────────────────────────────────
  → 판정: 🤖 에이전트
     단, '채널별 톤 변형' 한 토막은 순수 변환 → brand-voice 스킬로 분리
     ⇒ 3-1 과 같은 "에이전트 안의 스킬" 패턴
```

⏸ 다음으로 — "실행으로 넘어갈까요?"

---

## 2단계 · 실행

### 2-0. 사전 점검 (조용히)

Buffer MCP·Notion 통합·Discord webhook·Buffer 채널 연결 4가지를 조용히 점검한다. ❌ 항목만 골라 즉시 해결 — Buffer MCP 는 <https://publish.buffer.com> Access Token 생성 → `.env` 의 `BUFFER_ACCESS_TOKEN` + `.mcp.json` 의 `buffer` 서버(`npx @damusix/buffer-mcp`) 등록(신규 설치 시 세션 재시작 1회), Buffer 채널 연결은 대시보드에서 IG·FB·X 계정 연동(1개만 연결돼도 진행 가능), Notion 은 3-1 과 동일 절차, Discord webhook 은 아래 **📎 부록 · Discord webhook 추가하는 법** 참조.

```bash
claude mcp list 2>&1 | grep -i "buffer"                        # Buffer MCP
test -f "discord-bot/webhook-config.json" && echo "webhook ✅"
grep -q "BUFFER_ACCESS_TOKEN" .env 2>/dev/null && echo "token ✅"
grep -q "DISCORD_WEBHOOK_URL=" .env 2>/dev/null && echo "discord webhook ✅"
```

#### 📎 부록 · Discord webhook 추가하는 법 (webhook ❌ 일 때만)

> 웹훅은 봇 토큰 없이 **특정 채널에 메시지를 던지는 일방향 URL** 이다. 큐잉 확인·승인 요청 발송에 쓴다.
> 마케터(비개발자) 기준 5분. 한 번 만들면 모든 에이전트가 공용으로 쓴다.

```
STEP 1 · 채널 선택
   디스코드 서버에서 발송받을 채널 (예: #marketing-main) 준비
   ※ 없으면 채널 새로 생성 (+ 버튼)

STEP 2 · 웹훅 생성
   채널 옆 ⚙️ (채널 편집) → [연동] (Integrations) → [웹후크] → [새 웹후크]
   → 이름 입력 (예: "marketing-os") → [웹후크 URL 복사]
   ※ 모바일: 채널 길게 누름 → 편집 → 연동 → 웹후크

STEP 3 · .env 에 등록
   marketing-os/.env 파일에 한 줄 추가:
     DISCORD_WEBHOOK_URL=https://discord.com/api/webhooks/xxxx/yyyy
   (선택) 용도별 채널을 더 두려면 webhook-config.json 표준에 맞춰 추가:
     DISCORD_WEBHOOK_URL_ALERTS=...      # 임계치 위반·긴급
     DISCORD_WEBHOOK_URL_APPROVALS=...   # 발송·예산 승인 요청
     DISCORD_WEBHOOK_URL_RESEARCH=...    # 리서치 자동 발송
     DISCORD_WEBHOOK_URL_CS=...          # CS 응대 초안

STEP 4 · 발송 테스트 (HTTP 204 면 성공)
```
```bash
cd marketing-os && set -a; source .env; set +a
curl -s -o /dev/null -w "HTTP %{http_code}\n" \
  -H "Content-Type: application/json" \
  -X POST -d '{"content":"✅ marketing-os webhook 연결 완료"}' \
  "$DISCORD_WEBHOOK_URL"
```
```
STEP 5 · embed 표준 확인
   discord-bot/webhook-config.json 의 colors·embed_templates 를 따른다
   (큐잉 확인 = success 5763719 / 승인 요청 = warning 16705372).
```

⚠️ **보안** : 웹훅 URL = 사실상 비밀번호. `.env` 에만 두고 절대 커밋 금지 (`.gitignore` 등록 확인).
유출 의심 시 STEP 2 화면에서 [웹후크 삭제] 후 재발급.

### 2-1. 이 에이전트의 5요소 + 작동 구조

`open agents/part3-content/content-publisher.md` 로 펼쳐 **업무 → 에이전트 5요소**를 짚는다:

```
1) frontmatter : name + description
2) tools       : Notion · Buffer · Skill(brand-voice)   ← 이 에이전트만 Buffer 권한(최소 권한)
3) trigger     : /publish-this-week / /publish-next-batch
4) workflow    : Draft 조회 → [승인] → 채널별 변형 → 큐잉 → 상태 동기화
5) outputs     : Buffer 큐 · Notion(Scheduled) · Discord embed
→ 3-1 과 5요소 골격이 같다. tools·trigger·outputs 가 있으니 에이전트.
```

그 workflow(④)가 실제로 이 순서로 돈다:

```
🔄 에이전트 워크플로 (순서도)
  [Notion 콘텐츠 캘린더 : status="Draft"]
    → 디스코드에 Draft 목록 표로 승인 요청
    → ⏸ 항목별 reaction (✅ 큐잉 / ❌ 건너뜀)
    → 채널별 자동 변형 : IG 1500자+이모지 / X 280자 / LinkedIn 비즈니스 톤 / FB 500자 / TikTok 150자
    → Buffer 큐잉 (예약 시각 자동 배치)
    → Notion 상태 Draft → Scheduled + Buffer URL 저장
    → 디스코드 큐잉 확인 embed
```

에이전트 정의를 함께 펼쳐 새로 볼 3요소를 확인한다 (`open agents/part3-content/content-publisher.md`):
① frontmatter 의 tools : `mcp__buffer__*` (이 에이전트만 Buffer 권한 · 권한 최소화)
② 채널별 자동 변형 규칙 표 (길이·해시태그·톤이 채널마다 다름)
③ 에러 처리 표 (Buffer 미연결 → Skip + 경고 / 이미지 404 → Draft 롤백)
퀴즈: "X(트위터) 변형의 글자 수 제한과 해시태그 개수는?"

### 2-2. 데이터 준비

```
📊 데이터 모드를 선택하세요:

  [A] 샘플 데이터 모드 ⭐ 추천 · 촬영 기본
      sample-data/content-calendar-drafts.json 의 결로아 Draft 콘텐츠 3건을
      Notion "콘텐츠 캘린더" DB 에 자동 시딩. 중복 검출 시연용 행 1건 포함.

  [B] 실데이터 모드
      본인 Notion 의 기존 콘텐츠 캘린더에서 Draft 행 사용.
```

**[A] 샘플 모드** — 픽스처 `content-calendar-drafts.json` (브랜드: 결로아 Gyeolloa · 제품: 포어 토너 V2 / TONER-V2 · 캠페인: 21일 모공 챌린지) 을 읽어 Notion 에 시딩:
1. Notion DB **"콘텐츠 캘린더"** 생성 (콘텐츠 제목 title · 발행일 date · 채널 multi_select · 상태 select · Buffer URL · 이미지 URL)
2. Draft 3행 삽입 (발행일은 오늘 기준 +1d / +2d / +3d 로 환산)
   - ① "포어 토너 V2 론칭 캐러셀 : 모공이 달라지는 3단계" → IG·FB·X (+1d)
   - ② "21일 모공 챌린지 참여 안내 : 인증하면 정품 증정" → IG·X·TikTok (+2d)
   - ③ "성분 이야기 : PHA가 모공 케어에 적합한 이유" → LinkedIn·Blog·FB (+3d)
3. **중복 검출 시연 준비** : `duplicate_demo_row` — ①과 동일 제목의 행을 7일 이내 **Published** 상태로 1건 추가 (발행일 3일 전) → 에이전트가 중복 경고 발생
4. 시딩 결과 표 + DB URL 출력

**[B] 실데이터 모드** — 기존 캘린더 DB 검색 → Draft 행 수·이미지 URL 유무 확인 → 부족하면 샘플 전환 제안.

⏸ 시딩 결과 OK 받고 2-3 으로.

### 2-3. 실제 실행

```
▶ 에이전트 워크플로 단계별 실행:

  1. Notion 쿼리 : status="Draft"                  → 3건 표로 표시
  2. 중복 검사                                       → ① 행에서 ⚠️ 중복 경고 발생 (시연 포인트)
       → "그래도 진행 / 건너뜀" 사용자 선택
  3. 디스코드 #marketing-approvals 승인 요청 표 발송
  4. 항목별 승인                                     ⏸ 데모 모드 선택:
       [a] 디스코드 reaction 실제 대기 (30분 → 2분 단축)
       [b] 터미널에서 항목별 y/n ⭐ 촬영 추천
  5. 승인된 항목만 채널별 변형 생성                  → 변형 결과를 채널별로 나란히 표시
       (같은 원본이 IG/X/LinkedIn 에서 어떻게 달라지는지가 시연 하이라이트)
  6. Buffer 큐잉                                     → 게시물 URL 확보
  7. Notion 상태 업데이트 : Draft → Scheduled + Buffer URL
  8. 디스코드 큐잉 확인 embed
```

Buffer 채널이 미연결 상태로 진행하는 경우: 5번까지 시연 후 "큐잉 직전" 상태로 종료 가능 (건너뛰기 허용).

⏸ **승인 받은 뒤에만 실제 큐잉.** 각 단계 결과 확인 후 다음 단계.

---

## 3단계 · 활용 — 지금, 내 업무로

> 안내로 끝내지 않는다. **바로 "당신 콘텐츠"를 채널별로 변형해본다.**

### 적용 게이트 (능동 질문 ⏸)

```
🚀 그럼, 지금부터 내 업무에 적용해볼까요?

   결로아 Draft 자리에 당신 콘텐츠 1건만 넣으면 똑같이 작동합니다.
   아래 3가지만 알려주시면, 지금 바로 채널별 변형 미리보기를 만들어 드릴게요.

   ① 어떤 브랜드/업종인가요?            (예: 홈카페 원두 D2C)
   ② 운영 중인 채널은?                  (예: 인스타·X·블로그)
   ③ 지금 올리고 싶은 콘텐츠 1건은?     (제목 한 줄이면 충분)
```

→ 답을 받으면 : 그 콘텐츠를 **채널별로 즉석 변형**(IG 길게+이모지 / X 280자 / LinkedIn 비즈니스 톤)
   → 나란히 비교 미리보기 → (Buffer 연결 시) 큐잉까지.
→ "건너뛰기" 하면 아래 정착 가이드만 안내하고 마무리.

### 오래 쓰는 법 (적용 후 정착)
- **A. 실데이터로 교체** — 본인 Notion 콘텐츠 캘린더의 Draft 행으로 [B] 모드 가동. Buffer 에 본인 IG·FB·X 계정만 연결돼도 해당 채널만 큐잉된다.
- **B. 다른 클립과 연결** — 5-4 content-calendar 가 주간 30건을 Draft 로 적재하면, 그 출력이 곧 이 에이전트의 입력 (캘린더 → 퍼블리셔 순환 구조).
- **C. 자동 가동 (cron)** — `/publish-this-week` 명령으로 매주 정해진 요일에 Draft → 변형·큐잉 자동 실행.
- **D. 확장** — 채널별 변형 규칙(길이·해시태그·톤)을 본인 브랜드 채널 운영 정책에 맞게 수정 + 예약 시각 수동 조정 후 재큐잉.

📊 **산출물 3종**
- **Buffer** : 채널별 예약 게시물 N개 (큐 화면 확인)
- **Notion** : 상태 Scheduled 로 변경 + Buffer URL 저장
- **Discord** : 큐잉 확인 embed (총 게시물 수 + 채널 분포)

✅ 체크리스트
- [ ] 같은 원본이 채널별로 다르게 변형된 것을 비교 설명 가능
- [ ] 중복 경고가 왜 떴는지 이해
- [ ] ❌ 한 항목이 큐잉되지 않은 것 확인

🔁 **다음 클립**
- "3-3 실습 시작" : 뉴스레터 작성 스킬 만들기 (에이전트가 호출하는 스킬)
