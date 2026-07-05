# 클립 1-3. 트리거 하나로 전체 에이전트 팀이 가동되는 구조

## 한 명령으로 30개를 움직이는 법

```
사용자 (디스코드)
  ↓ /ax-team-run weekly
[Discord MCP / Hook]
  ↓
[Orchestrator]
  ↓ 4 페이즈 라우팅
[30 에이전트가 페이즈별 협업]
  ↓
[Discord 채널] 종합 embed
```

## 학습 목표 (대단원)
- **AX 시스템 전체를 1줄 명령으로 가동**
- 자동화 cron 3개로 24시간 운영
- 디스코드 봇 인바운드·아웃바운드 완성

## 핵심 파일 (이미 만들어져 있음)
- [`commands/ax-team-run.md`](../../../commands/ax-team-run.md) — 4 페이즈 정의
- [`agents/orchestrator.md`](../../../agents/orchestrator.md) — 라우팅 로직
- [`discord-bot/`](../../../discord-bot/) — 봇 연결
- [`automation/`](../../../automation/) — cron 3개

→ [`실습.md`](실습.md)

---

## 실습 스킬 — 에이전트 팀을 디스코드(클로드 채널)로 연결

이 대단원 실습은 "명령어로 트리거를 거는 것"에서 한 걸음 더 나아가, **내가 만든 에이전트 팀(30개)을 디스코드 채널 하나로 꺼내 — 나뿐 아니라 팀원도 폰에서 함께** 부르게 만드는 것을 시연합니다. (기준 문서: [`에이전트팀-디스코드-팀연동-가이드.md`](../에이전트팀-디스코드-팀연동-가이드.md))

실행은 전용 스킬로 진행합니다. **"이 폴더에 (저장소) 에이전트 세팅하고 클로드 채널 연동하자"** 라고 말하면
[github-team-to-discord/SKILL.md](github-team-to-discord/SKILL.md) 의 4-Part 흐름이 시작됩니다:
Part 1 (clone → agents/ 로 팀 모으기) →
**Part 2 (오케스트레이션 에이전트 가이드 문서 `orchestrator.md` 구축 ⭐ 핵심)** →
Part 3 (클로드 채널 연동 — 방법은 기존과 동일, "그 폴더만 지정") →
Part 4 (폰에서 요청 → 라우팅 → 회신 시연).

채널 연동 자체는 `discord-channels-setup` 과 동일하며, 이 스킬의 핵심 산출물은 **팀을 지휘하는 orchestrator.md 가이드 문서**입니다.
손으로 따라가는 요약판은 [`실습.md`](실습.md) 를, 팀 공용 보안·운영 함의는 기준 문서를 참조하세요.
