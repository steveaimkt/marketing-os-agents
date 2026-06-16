# 클립 1-2. 콘텐츠 자동 업로드 에이전트: 콘텐츠 작성 → Buffer 예약하기

## 한 줄 요약
노션 콘텐츠 캘린더의 **Draft 상태 콘텐츠를 5개 SNS 채널에 동시 변형·예약**합니다. 1주일치 콘텐츠 큐잉이 명령 1줄.

## 무엇을 만드나
- 에이전트 정의: [`agents/part3-content/content-publisher.md`](../../../agents/part3-content/content-publisher.md)
- 의존: Notion MCP, Buffer MCP, Discord Webhook, (선택) `brand-voice` 스킬

## 핵심 디자인 결정
- **채널별 자동 변형** — 같은 원본을 IG는 1500자+이모지, X는 280자, LinkedIn은 비즈니스 톤으로
- **승인 게이트** — Draft 목록을 디스코드에 표로 띄우고, ✅ 리액션 받은 항목만 큐잉
- **중복 방지** — 7일 이내 동일 내용 검출 시 경고

## 워크플로

```
[노션 캘린더 DB: status="Draft" 행]
      ↓ 디스코드에 승인 요청
[사용자 ✅]
      ↓
[채널별 변형 — 길이/해시태그/톤]
      ↓
[Buffer 큐잉]
      ↓
[노션: status → Scheduled + Buffer URL 저장]
      ↓
[디스코드 큐잉 확인 embed]
```

→ [`실습.md`](실습.md)

---

## 실습 스킬

촬영·실습은 전용 스킬로 진행합니다. **"3-2 실습 시작"** 이라고 입력하면
[실습-3-2-content-publisher/SKILL.md](실습-3-2-content-publisher/SKILL.md) 의 게이트 흐름 (점검·설치 → 안내 → 데이터 준비 → 에이전트 열람 → 시연 → 산출물 확인) 이 시작됩니다.
샘플 데이터는 [실습-3-2-content-publisher/sample-data/](실습-3-2-content-publisher/sample-data/) 에 포함되어 있습니다.
