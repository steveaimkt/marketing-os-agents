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

촬영·실습은 전용 스킬로 진행합니다. **"10-3 실습 시작"** 이라고 입력하면
[실습-10-3-trigger-system/SKILL.md](실습-10-3-trigger-system/SKILL.md) 의 게이트 흐름이 시작됩니다:
① 소개 (3층 구조 + "채널은 폴더가 아니라 세션에 붙는다" 오해 교정 + 전제 점검) →
② 실행 (PART A 1인 봇↔클로드채널 연결 7스텝 → PART B 팀원 allowlist 확장 → 폰 라이브 시연) →
③ 활용/마무리 (팀 공용 보안 3대 고려 + OPERATIONS.md 팀 매뉴얼 + 🎉 강의 종료 체크리스트).

샘플 데이터(팀 접근 계획·폰 시연 대본·OPERATIONS.md 템플릿)는 [실습-10-3-trigger-system/sample-data/](실습-10-3-trigger-system/sample-data/) 에 포함되어 있습니다.
