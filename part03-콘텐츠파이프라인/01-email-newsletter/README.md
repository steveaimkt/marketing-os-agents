# 클립 1-1. 이메일 자동 발송 에이전트: 트렌드 → 뉴스레터 → Gmail 발송하기

## 한 줄 요약
**매주 월요일 09:00**, Claude가 지난 주 트렌드를 모아 뉴스레터 한 통을 작성·발송합니다. 1인 마케터의 1~2시간 절약.

## 무엇을 만드나
- 에이전트 정의: [`agents/part3-content/email-newsletter.md`](../../../agents/part3-content/email-newsletter.md)
- 의존: Gmail MCP (Claude.ai 통합), Notion MCP, Discord Webhook, `newsletter-writing` 스킬

## 워크플로 (한눈에)

```
[Notion 트렌드 DB]
      ↓
[5개 선별]
      ↓
[newsletter-writing 스킬 호출]
      ↓
[디스코드 #marketing-approvals 에 미리보기 발송]
      ↓ (15분 reaction 대기)
[Gmail 발송] → [Notion 아카이브] → [Discord 발송 확인]
```

## 핵심 안전 원칙
**자동 발송 직전에 반드시 사용자 승인 단계.** 디스코드에 미리보기를 띄우고 reaction(✅ 또는 ❌)을 기다린다. 15분 미응답 = 발송 안 함.

## 사전 준비물
- Gmail 통합 활성화 (Claude.ai)
- Notion DB: "주간 트렌드" + "뉴스레터 아카이브"
- (없으면) `trend-scanner` 에이전트를 Part 4에서 먼저 만들기

## 학습 포인트
- **에이전트 정의 파일 (.md)의 구조**: YAML frontmatter + 시스템 프롬프트 + 워크플로 + 산출물 표준 + 에러 처리
- **승인 게이트** 패턴: 자동화의 단계 중 한 곳에 사용자 reaction을 강제

→ [`실습.md`](실습.md)

---

## 실습 스킬

촬영·실습은 전용 스킬로 진행합니다. **"3-1 실습 시작"** 이라고 입력하면
[실습-3-1-email-newsletter/SKILL.md](실습-3-1-email-newsletter/SKILL.md) 의 게이트 흐름 (점검·설치 → 안내 → 데이터 준비 → 에이전트 열람 → 시연 → 산출물 확인) 이 시작됩니다.
샘플 데이터는 [실습-3-1-email-newsletter/sample-data/](실습-3-1-email-newsletter/sample-data/) 에 포함되어 있습니다.
