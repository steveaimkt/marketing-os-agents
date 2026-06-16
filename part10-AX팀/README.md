# Part 10. AX 협업 — 에이전트 1개에서 에이전트 팀으로

> 이 Part에서 배우는 것: **30개 에이전트를 1개처럼 운영하는 AX 시스템**. 트리거 하나로 4 페이즈가 자동 진행되는 진짜 마케팅 OS.

## AX란 무엇인가

| | AI 비서 (에이전트 1개) | AX 시스템 (에이전트 팀) |
|---|---|---|
| 모습 | 1명의 만능 AI | 디렉터 1 + 전문가 30 |
| 컨텍스트 | 모든 워크플로 로드 → 토큰 폭증 | 디렉터는 라우팅만, 전문가는 호출 시에만 |
| 권한 | 모두 한 곳에 → 사고 시 폭발반경 큼 | 에이전트별 권한 분리 |
| 디버깅 | 어디서 실패했는지 추적 어려움 | 에이전트별 로그·산출물 분리 |
| **사용자 UX** | "마케팅 봇 한 개" | **"마케팅 봇 한 개" (동일!)** |

**핵심 결론**: AX 시스템은 사용자에게 "봇 1개"로 보이지만, 내부는 30개 전문가가 일하는 팀.

## 3개 클립

| 클립 | 내용 |
|---|---|
| 1-1 | AX란 무엇인가 (이론) |
| 1-2 | 에이전트 팀 역할 설계 (Part 1~9 통합 그림) |
| 1-3 | **트리거 하나로 전체 팀 가동** (실습 대단원) |

## 4 페이즈 가동 흐름 ([`/ax-team-run weekly`](../../commands/ax-team-run.md))

```
[Phase 1] 리서치 (병렬, 5분)
  trend-scanner / competitor-monitor / ad-reference-collector / voc-analyzer
      ↓
[Phase 2] 분석 (병렬, 5분)
  ga4-analyzer / meta·google·naver-ads / ad-performance-checker / ltv-analyzer
      ↓
[Phase 3] 합성 (순차, 3분)
  3media-integrated-reporter
  ga4-html-report → ga4-notion-publisher
  content-calendar
  ad-copy-ab (10패턴)
      ↓
[Phase 4] 발송 (병렬, 2분)
  Discord #marketing-os: 종합 embed + HTML + 노션 링크
  Discord #marketing-approvals: 큐잉 승인 요청
  (선택) Gmail stakeholder
```

**전체 약 15~20분, 사용자는 디스코드 명령 1줄만.**

## 채널 구조 (Part 2 Ch4 재확인)

```
서버: marketing-os
├── #marketing-os         ← 메인 컨트롤 (사용자 ↔ 봇)
├── #marketing-alerts     ← 광고 임계치 (ad-performance-checker)
├── #marketing-approvals  ← 발송·예산 승인 게이트
├── #marketing-research   ← 리서치 자동 발송
└── #marketing-cs         ← CS 응대 초안
```

→ [`01-ax-introduction/`](01-ax-introduction/)
