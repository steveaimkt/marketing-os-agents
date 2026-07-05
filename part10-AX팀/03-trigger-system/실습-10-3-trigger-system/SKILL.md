---
name: 실습-10-3-trigger-system
description: |
  Part 10 클립 10-3 (에이전트 팀을 디스코드=클로드 채널로 연결) 실습 시연 스킬 — 강의 대단원(캡스톤). 사용자 한 줄 명령 →
  ① 소개 (3층 구조 멘탈모델 + "내 팀은 지금 GitHub에 흩어져 있다" + "채널은 폴더가 아니라 세션에 붙는다" 오해 교정 + 전제 점검) →
  ② 실행 (PART A: A-0 GitHub에서 팀 가져오기[clone→agent.md 복사→orchestrator.md 생성] → A-1~A-7 봇↔클로드채널 연결 → PART B 팀원 allowlist 확장 → 폰 라이브 시연) →
  ③ 활용/마무리 (보안 3대 고려 + OPERATIONS.md 팀 매뉴얼 + 🎉 강의 종료 체크리스트).
  흐름 : ① 소개 ② 실행 ③ 활용/마무리. 자동 실행 금지. 단계마다 답 받고 다음.
  기준 문서 : curriculum/part10-AX팀/에이전트팀-디스코드-팀연동-가이드.md (이 스킬은 그 가이드의 실습 진행판).
  에이전트 소스 : https://github.com/steveaimkt/marketing-os-agents (Part 3~10 클립별 agent.md) + MCP는 marketing-os-mcp-setup.
  ⚠️ 실제 시스템(git clone·파일 복사·봇 토큰·세션·allowlist)을 다루므로 특히 단계마다 사용자 승인 후 진행.

  자동 호출 트리거:
  - **"10-3 실습 시작"** ⭐ 주요 트리거
  - "디스코드 팀 연동 실습" / "클로드 채널 연결 실습 시작하자"
  - "에이전트 팀 디스코드 연결" / "팀 공용 봇 실습"
  - "GitHub 에이전트 디스코드 연동" / "깃허브 팀 가져와서 봇 연결"
  - "trigger-system 실습" / "AX 대단원 실습" / "Part 10 마지막 실습" / "강의 마지막 실습"

  동작: 한 줄 → 3 단계 인터랙티브 → (PART A) A-0 GitHub clone→agent.md 복사→orchestrator.md 생성→CLAUDE.md 확인
  → 봇 생성→intent→초대→플러그인→configure→`--channels`→페어링→allowlist 잠금
  → (PART B) 팀원 페어링 추가 + 채널 멘션 정책 + 폰에서 "@봇 요청" 라이브 도착 →
  보안 3대 고려 + OPERATIONS.md + 🎉 강의 종료 체크리스트 → 강의 전체 종료·마무리.
---

# Part 10 / 10-3 · 에이전트 팀을 디스코드(클로드 채널)로 연결 : 강의 대단원(캡스톤)

> Part 3~9에서 배운 **에이전트 팀(30개)**을 → **GitHub에서 내 프로젝트로 가져오고** → **디스코드 채널 하나**로 → **나뿐 아니라 팀원도 폰에서 함께** 부를 수 있게 만든다.
> 핵심 학습 목표 : ① 3층 구조 멘탈모델(입구=채널·두뇌=세션·팀=서브에이전트) ② PART A GitHub 팀 가져오기 + 1인 연결 ③ PART B 팀 공용 확장 + 보안 3대.
> ⛔ 자동 실행 금지. git clone·파일 복사·봇 토큰·세션·allowlist 등 실제 시스템을 바꾸므로 **단계마다 사용자 답을 받은 뒤에만** 다음으로.
> 📄 기준 문서 : `curriculum/part10-AX팀/에이전트팀-디스코드-팀연동-가이드.md` (이 스킬은 그 가이드의 실습 진행판)
> 🐙 에이전트 소스 : `https://github.com/steveaimkt/marketing-os-agents` · MCP는 `marketing-os-mcp-setup`

## 진행 흐름 (3 단계)

```
1단계  소개       3층 구조 + "내 팀은 GitHub에 흩어져 있다" + "채널은 폴더가 아니라 세션에 붙는다" 오해 교정 + 전제 점검   ⏸ 답 대기
2단계  실행       PART A(A-0 GitHub 팀 가져오기 → A-1~A-7 봇↔채널 연결) → PART B(팀원 allowlist 확장) → 폰 라이브 시연   ⏸ 답 대기
3단계  활용/마무리  보안 3대 고려 + OPERATIONS.md 팀 매뉴얼 + 🎉 강의 종료 체크리스트                                    ⏸ 선택
```

---

## 1단계 · 소개

```
🏁 강의 대단원입니다. 지금까지 배운 30 에이전트 + 5 스킬 + 12 MCP 를 "팀이 쓰는 창구" 하나로 엽니다.

🎯 하는 일
  "터미널에 앉은 나 혼자만 쓰던 에이전트 팀을 → 디스코드 채널로 꺼내
   폰에서, 그리고 팀원까지 함께 부르게 만든다."
  GitHub 에이전트 → 내 프로젝트(agents/ + orchestrator) → 디스코드 봇(다리) → 내 세션(트루먼) → 30 에이전트로 라우팅.

⏱ Before vs After
  · Before : 에이전트 팀은 GitHub 저장소에 조각조각 흩어져 있고, 내 터미널 안에서만 돈다. 팀원은 나에게 부탁 → 내가 대신 실행
  · After  : #팀-마케팅봇 채널에서 팀원이 "@봇 지난주 ROAS 뽑아줘" → 폰으로 결과 도착
```

🐙 **먼저 짚기 — 내 팀은 지금 어디에 있나**

```
  Part 3~9에서 배운 에이전트들은 GitHub 저장소에 클립별로 흩어져 있습니다.
    · github.com/steveaimkt/marketing-os-agents
      part03~part10/**/agent.md  ← 에이전트 정의 조각들 (그대로 사용 가능)
    · github.com/steveaimkt/marketing-os-mcp-setup  ← MCP(.mcp.json·.env) 설정

  ⚠️ 이 저장소에 "없는" 것 2가지 (그래서 A-0에서 우리가 만든다):
    ① agents/ 폴더로 모아진 팀     — clip별 agent.md 를 한 폴더로 복사해야 세션이 인식
    ② orchestrator.md (라우팅 두뇌) — 저장소엔 조각만 있고 "누구에게 보낼지" 정하는 두뇌가 없음

  🧩 즉 이번 클립은 : 흩어진 조각(GitHub) → 한 팀(agents/) → 두뇌(orchestrator) → 창구(디스코드) 로 잇는 마지막 조립.
```

🔑 **가장 흔한 오해 — 강의에서 반드시 짚기**

```
  ❌ "에이전트 폴더가 디스코드에 연결된다"
  ✅ 정확히는 : 클로드 채널은 폴더가 아니라 실행 중인 `claude --channels` 세션에 붙는다.
     그 세션을 프로젝트 폴더 안에서 켜기 때문에 → 세션이 그 폴더의
     CLAUDE.md · agents/ · skills/ · .mcp.json 을 자동으로 쓴다.

  🧠 한 문장 : "디스코드는 세션에 붙는다. 세션은 폴더에서 켠다. 그래서 폴더의 에이전트가 딸려 온다."
  → 그래서 A-0에서 GitHub 팀을 "프로젝트 폴더 안"으로 가져오는 것이 연결의 실체다.
```

🏛 3층 구조 (연결의 실체)

```
   🐙 GitHub 저장소  (marketing-os-agents / -mcp-setup)  ← 팀의 원본 소스
        │  A-0에서 clone → agents/ 로 복사 → orchestrator.md 생성
        ▼
   📱 팀원들의 폰 디스코드  (DM 또는 채널 메시지)
        ▼
  ① 입구 = 디스코드 채널     ← 클로드 채널 플러그인이 만드는 '다리' · allowlist 로 통제
        ▼
  ② 두뇌 = 실행 중인 세션    ← `claude --channels` 로 켜둔 그 세션 (오케스트레이터 = 트루먼)
        │                      프로젝트 폴더에서 켜야 CLAUDE.md · agents/ · .mcp.json 자동 로드
        ▼  자연어 라우팅
  ③ 팀 = 서브에이전트 30개   ← 호출될 때만 로드 (토큰 절약 · 권한 분리) + MCP + 로컬도구
```

🔌 전제 조건 (트리거 시 점검 · 연동 전에 준비돼 있어야 함)

```bash
git --version                   # A-0 clone 에 필요
test -f ".mcp.json"             && echo "외부 연결(.mcp.json) ✅" || echo ".mcp.json ❌ → marketing-os-mcp-setup 선행"
test -f "CLAUDE.md"             && echo "프로젝트 헌법 ✅"        || echo "CLAUDE.md ❌ (A-0에서 확인)"
test -f "agents/orchestrator.md" && echo "오케스트레이터(두뇌) ✅" || echo "오케스트레이터 ❌ (A-0에서 생성)"
claude --version                # ≥ 2.1.80 필요
bun --version                   # 채널 플러그인 = Bun 스크립트 → 필수
```

```
  | # | 항목 | 확인 | 없으면 |
  |---|---|---|---|
  | ① | 에이전트 팀   | agents/ 에 orchestrator + 전문가 30 | ⭐ A-0 에서 GitHub clone → 생성 |
  | ② | 외부 연결     | .mcp.json (12개 서버)              | marketing-os-mcp-setup 저장소 선행 |
  | ③ | 프로젝트 헌법 | 루트 CLAUDE.md                     | A-0 에서 없으면 최소 골격 생성 |
  | ④ | 런타임        | git · claude ≥ 2.1.80 · bun         | 업데이트 / Bun·git 설치 |
  | ⑤ | 인증          | claude.ai(Pro/Max/Team) 또는 Console API 키 | Bedrock/Vertex/Foundry는 채널 불가 |
```

📐 **이건 시스템 오케스트레이션** — 하나의 도구·에이전트가 아니라
  **오케스트레이터(라우팅) + 서브에이전트(도메인 30) + 스킬(패턴 5)의 합**이다.
  이번 클립은 GitHub에 흩어진 팀을 모아 "팀이 함께 쓰는 창구(디스코드)"에 꽂는 마지막 조립이다.

💡 핵심 포인트
  · 팀의 원본은 **GitHub** — A-0에서 clone 해 내 프로젝트로 가져오고 두뇌(orchestrator)를 얹는다
  · 채널 플러그인은 **다리**일 뿐 — 진짜 두뇌는 프로젝트 폴더에서 켠 `--channels` 세션
  · 제어는 **3중 게이트** : 발신자 allowlist(플러그인) → 세션 옵트인(`--channels`) → 조직 channelsEnabled(관리자)
  · 🛡 팀 공용 = 관리자의 단일 세션·단일 인증 공유 → 3단계 보안 고려를 반드시 이해하고 확장

⏸ 여기까지 이해되셨으면 "2단계" 라고 답해 주세요.

---

## 2단계 · 실행

### 2-0 · 사전 점검
1단계 전제 조건 표에서 ❌ 인 항목을 먼저 해결한다.
- **②(.mcp.json)** 가 없으면 `marketing-os-mcp-setup` 저장소를 먼저 따라가 MCP를 붙인다 (에이전트가 부를 외부 도구가 없으면 반쪽).
- **①(agents/)·③(CLAUDE.md)·④(orchestrator)** 는 이번 **A-0**에서 GitHub로부터 만든다.
⚠️ 이 실습은 git clone·파일 복사·봇 토큰·세션·allowlist 등 실제 시스템을 만지므로, 각 명령은 **사용자 승인 후** 실행한다.

### 2-1 · 작동 구조 (연결선을 직접 잇는다)
```
  [PART A] A-0 GitHub에서 팀 가져오기(clone → agent.md 복사 → orchestrator.md 생성 → CLAUDE.md 확인)
             → 봇 만들기 → 토큰 → 서버 초대 → 플러그인 설치 → configure(토큰 등록)
             → `--channels` 세션 재시작(★핵심) → 페어링 → allowlist 잠금
                = "GitHub 팀을 나 1명이 디스코드로 쓰는" 상태 완성
  [PART B] 팀원이 메시지 → 페어링 코드 → 관리자가 `pair` → allowlist 추가
             → 채널 멘션 정책 → "팀 공용 봇" 완성
```
📄 상세 인터랙티브 버전은 `discord-channels-setup` 스킬 · 기준 문서(가이드 §3~4) 참조.

퀴즈: "GitHub 저장소를 clone 하고 `.mcp.json` 에 등록만 하면 봇이 응답할까?"
(답: 아니오. **agent.md 들을 agents/ 로 모으고 orchestrator.md 를 얹은 프로젝트 폴더에서 `claude --channels …` 세션을 켜야** 봇이 그 세션에 붙어 응답한다.)

### 2-2 · 모드·데이터 준비

```
📊 연결 모드:

  [A] 신규 연결 모드 ⭐ (팀이 아직 로컬에 없음) → A-0(GitHub 가져오기) 부터 (2-3)
      GitHub clone → agents/ 구성 → orchestrator 생성 → 봇 7스텝. 촬영 시 "봇 🟢 온라인" 장면이 하이라이트.

  [B] 팀 확장 모드 (봇은 이미 1인 연결됨) → PART B 로 (2-4)
      이미 agents/ 팀 + `--channels` 봇이 있다 → 팀원 추가만.

  📄 보조 픽스처 : sample-data/team-access-plan.md (팀원 3명 · 신뢰수준 · 멘션 정책 · MCP 접근 범위 검토표)
                 sample-data/team-bot-demo.md    (폰 라이브 시연 대본 — 팀원 2명 요청 → 라우팅 → 회신)
```

⏸ A/B 답 받고 진행. (A → 2-3, B → 2-4)

### 2-3 · PART A — GitHub 팀 가져오기 → 봇 ↔ 클로드 채널 연결 (1인 기준)

> ⚠️ 토큰은 화면·채팅에 붙여넣지 말 것. 각 스텝은 사용자 승인 후.

#### A-0. GitHub에서 에이전트 팀 가져오기 ⭐ (이번 클립의 새 관문)

```
  ⓐ 저장소 clone (프로젝트 폴더 밖 임시 위치)
     git clone --depth 1 https://github.com/steveaimkt/marketing-os-agents.git /tmp/mos-agents

  ⓑ 클립별 agent.md 를 내 프로젝트 agents/ 로 복사 (파일명 = 클립 이름)
     mkdir -p agents
     find /tmp/mos-agents -name agent.md | while read f; do
       clip=$(basename "$(dirname "$f")")          # 예: 01-email-newsletter
       name=$(echo "$clip" | sed -E 's/^[0-9]+-//') # → email-newsletter
       cp "$f" "agents/${name}.md"
     done
     ls agents/    # → email-newsletter.md, content-publisher.md, … 30개 확인

  ⓒ orchestrator.md (라우팅 두뇌) 생성 ★ 저장소엔 없으므로 여기서 만든다
     → agents/orchestrator.md 에 "요청 유형 → 담당 에이전트" 라우팅 표 + 승인 게이트(조회=자동/발행=승인/삭제·예산=금지) 작성.
       (마케팅 OS 헌법의 오케스트레이터 원칙을 따른다 — 입구 1개·두뇌 1개.)

  ⓓ CLAUDE.md 확인/생성
     test -f CLAUDE.md || echo "→ 프로젝트 정체성·라우팅 규칙 최소 골격 생성"
```

> 💡 A-0가 끝나면 "GitHub의 흩어진 조각"이 → "내 프로젝트 폴더 안의 한 팀 + 두뇌"가 된다.
>    이제 이 폴더에서 `--channels` 세션을 켜면(A-6) 팀이 통째로 딸려 온다.

⏸ agents/ 에 팀 + orchestrator.md 가 놓인 것을 확인했으면 "A-1" 로.

#### A-1 ~ A-7. 봇 ↔ 클로드 채널 연결

```
  A-1. 봇 만들기 + 토큰
       discord.com/developers/applications → New Application → Bot → Reset Token → 복사
       (⚠️ 토큰은 1번만 보임 · 안전한 곳에)

  A-2. Message Content Intent 켜기 ⭐ (자주 빠뜨림)
       Bot → Privileged Gateway Intents → Message Content Intent ON → Save
       (꺼져 있으면 봇이 페어링 코드에 무응답)

  A-3. 서버에 초대 (권한 6개)
       OAuth2 → URL Generator → Scopes: bot
       권한: View Channels · Send Messages · Send Messages in Threads
             · Read Message History · Attach Files · Add Reactions
       생성 URL → 새 탭 → 내 서버 선택 → 승인

  A-4. 플러그인 설치 (Claude Code 안에서)
       /plugin install discord@claude-plugins-official
       /reload-plugins
       → /discord: 입력 시 configure·access 자동완성 뜨면 성공

  A-5. 봇 토큰 등록
       /discord:configure <복사한 토큰>
       → ~/.claude/channels/discord/.env 에 저장

  A-6. `--channels` 로 세션 재시작 ⭐ 가장 중요
       # 반드시 A-0에서 팀을 모은 프로젝트 폴더(agents/·CLAUDE.md 있는 곳)에서
       claude --channels plugin:discord@claude-plugins-official
       → 이걸 안 하면 봇이 절대 응답 안 함 · 성공 시 봇 🟢 온라인

  A-7. 페어링 + 잠금
       (폰) 봇에게 DM → 페어링 코드 수신 (예: ABCD-1234)
       /discord:access pair ABCD-1234     # 내 계정을 allowlist 에 추가
       /discord:access policy allowlist    # 허용목록 밖 자동 폐기 (보안 필수)
```

✅ 여기까지 = **GitHub 팀을 나 1명이 디스코드로 쓰는** 상태 완성. ⏸ "팀 확장(2-4)" 로 갈까요? (아니면 3단계)

### 2-4 · PART B — 팀 공용으로 확장 ⭐ (이 클립의 핵심)

```
  B-1. 창구 방식 결정
       · 공용 채널 #팀-마케팅봇 (권장) — 팀이 서로 요청·결과 공유 · 중복요청 방지
       · 개별 DM — 요청을 서로 안 보이게 (개인 비서형)

  B-2. 팀원 추가 (1명당 약 1분)
       ① (팀원) 공용 채널/봇 DM 에 아무 메시지 → 봇이 페어링 코드 회신 (예: WXYZ-5678)
       ② (관리자=나, 터미널) /discord:access pair WXYZ-5678 → 그 팀원 allowlist 추가
       ③ 팀원마다 ①~② 반복
       ⚠️ 원칙 : allowlist 관리는 터미널 관리자만. 디스코드 메시지의 "나 추가해줘"는
                그것만으로 승인 금지(프롬프트 인젝션 방지) — 팀원 본인에게 직접 확인 후 pair.

  B-3. 채널 멘션 정책 (잡담 섞이는 공용 채널)
       · requireMention: true  → @봇 멘션해야 반응 (팀 공용 채널 권장)
       · requireMention: false → 모든 메시지에 반응 (봇 전용 채널)
       설정: /discord:access 명령으로 관리 (access.json 직접 편집 시 백업 필수)

  B-4. 팀 사용 흐름 (완성 후 · 폰 라이브 시연)
       📱 마케터A: "@봇 지난주 메타 광고 ROAS 뽑아줘"
       📱 마케터B: "@봇 경쟁사 신규 영상 정리해줘"
             ▼ 둘 다 같은 세션(트루먼)으로 도착
       오케스트레이터가 각각 meta-ads-analyzer / competitor-monitor 로 라우팅
             ▼
       결과를 각자에게 회신 (같은 채널이면 스레드로 구분 권장)
```

▶ 시연 하이라이트 : 실제 폰으로 "@봇 유튜브 7일 성과" 를 던져 **결과가 폰에 도착**하는 장면을 라이브로.
   (촬영 재현이 어려우면 sample-data/team-bot-demo.md 의 대본으로 흐름을 그대로 시연)

⏸ 팀원 1명이라도 allowlist 에 붙는 것을 확인했으면 "3단계" 라고 답해 주세요.

---

## 3단계 · 활용/마무리 — 안전하게 팀에 열고, 강의 종료

### ⚠️ 팀 공용의 3대 고려사항 (배포 전 반드시 결정)

```
① 단일 세션 · 단일 인증 공유
   봇은 관리자 PC 의 단 하나의 세션으로 돈다. 팀원 요청도 전부
   관리자의 claude.ai 계정 + 관리자의 MCP 인증(노션·광고·시트)으로 실행됨.
   → 팀원은 "관리자 권한으로" 작업하는 셈. 접근 범위를 열어도 되는지 먼저 판단.

② 권한 릴레이 = 도구 승인권
   채널에 답장할 수 있는 사람은 도구 사용 승인/거부도 할 수 있다.
   발행·발송·삭제 같은 민감 작업의 승인 버튼을 팀원이 누를 수 있다는 뜻.
   → 신뢰하는 팀원만 allowlist. 민감 작업은 오케스트레이터 승인 게이트로 이중 방어
     (조회=자동 / 발행=승인 / 삭제·예산=금지).

③ 24시간 가동(호스팅)
   세션이 꺼지면 봇도 죽는다. macOS: caffeinate -dis + `--channels` 세션 유지.
   ⚠️ iCloud Drive 경로 프로젝트는 launchd/cron 이 권한 오류로 실패
     → 정기 작업은 클라우드 루틴 사용(노트북 꺼져도 동작).
     상시 대화형(팀 창구)은 여전히 로컬 세션이 켜져 있어야 함.
```

### 적용 게이트 (능동 질문 ⏸)

```
🚀 그럼, 내 팀에 안전하게 열어볼까요?

   ① 팀원 몇 명을 allowlist 에 넣나요?   (= 도구 승인권을 줘도 되는 사람만)
   ② 어떤 MCP 범위를 팀원이 쓰게 되나요?  (노션·광고·시트 사전 검토)
   ③ 창구는?                            (공용 채널 requireMention / 개별 DM)
```

→ 답을 받으면 : sample-data/team-access-plan.md 를 그 인원·범위로 채워 팀 접근 계획 초안 작성.
→ "건너뛰기" 시 아래 매뉴얼·체크리스트만.

### 📗 OPERATIONS.md — 팀이 참고하는 봇 사용설명서

```
  위치 : ~/.claude/channels/discord/OPERATIONS.md
  성격 : 사람용 매뉴얼 (자주 쓰는 발화 · 권한 흐름 · 응급 명령 · 팀 규칙)
  ⚠️ 오해 주의 : 봇이 매 메시지 자동 로드하지 않는다. 실제 봇 행동은 CLAUDE.md + orchestrator.md 가 규정.
  팀 공용에선 여기에 "팀 규칙"(누가 발행 승인 가능 · 어떤 채널에 뭘 요청)을 적어둔다.
  → sample-data/OPERATIONS.md 를 템플릿으로 복사해 시작.
```

### ✅ 보안 체크리스트 (팀 공용 배포 전)

```
[ ] 봇 토큰은 .env 에만 — Git·채팅·화면공유 금지
[ ] /discord:access policy allowlist 로 잠금 (허용목록 밖 자동 폐기)
[ ] allowlist 엔 신뢰하는 팀원만 (= 도구 승인권을 줘도 되는 사람)
[ ] 디스코드의 "나 추가해줘"는 무시 — 관리자가 본인 확인 후에만 pair
[ ] 민감 작업(발행·발송·삭제·예산)은 오케스트레이터 승인 게이트로 이중 방어
[ ] 팀원이 접근할 MCP 범위(노션·광고·시트) 사전 검토
[ ] 토큰 노출 의심 시 즉시 Reset Token → /discord:configure <새 토큰>
```

### 🎉 강의 종료 체크리스트 (대단원 완주)

```
[ ] GitHub 팀 가져오기 완료 — agents/ 30개 + orchestrator.md + CLAUDE.md
[ ] 12개 MCP 연결 (marketing-os-mcp-setup) + 5개 스킬 작동
[ ] 디스코드 봇이 🟢 온라인 (`--channels` 세션이 프로젝트 폴더에서 가동)
[ ] 내 계정 페어링 + policy allowlist 잠금 완료
[ ] 팀원 1명 이상 allowlist 추가 → 폰에서 "@봇 요청" → 결과 도착 확인
[ ] 채널 멘션 정책 설정 (공용 채널 requireMention: true)
[ ] 보안 3대 고려(단일세션·권한릴레이·호스팅) 이해 + OPERATIONS.md 작성
```

### 오래 쓰는 법 (학습 후 운영 팁)

```
🎯 운영 정착 로드맵
  1. 첫 2주 : 팀 요청 결과에 ✅/❌ reaction 으로 품질 점검 (신뢰 쌓기)
  2. 3주~   : 신뢰가 쌓인 작업(FAQ 응대 등)부터 일부 자동 발송 허용
  3. 분기마다 : brand-guidelines 재실행 → 브랜드 톤 업데이트 · GitHub 저장소 pull 로 팀 최신화
  4. 연 1회 : marketing-calendar-builder 로 다음 해 계획 수립

🏁 강의 전체 종료
   축하합니다 — GitHub에 흩어져 있던 30개 에이전트 팀을 한 폴더로 모으고 두뇌를 얹어,
   이제 팀 전체가 폰에서 함께 부릅니다.
   "GitHub 조각 → 한 팀 → 두뇌 1개 → 창구 1개" 가 디스코드 채널 하나로 완성됐습니다.
   운영 사례를 노션에 기록해두면 다음 분기 보고서가 더 정확해집니다.
```
