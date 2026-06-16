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
