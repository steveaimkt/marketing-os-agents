# 클립 1-1. 경쟁사 모니터링 에이전트

## 한 줄 요약
**매일 09:00 자동으로** 등록 경쟁사 5~10개의 사이트·SNS·광고를 스캔하고, 어제 대비 변경점을 디스코드와 노션에 정리합니다.

## 에이전트
[`agents/part4-research/competitor-monitor.md`](../../../agents/part4-research/competitor-monitor.md)

## 핵심 디자인
- **diff 기반** — 어제 스냅샷과 텍스트 비교, 변경점만 보고
- **카테고리 자동 분류** — 신제품/가격/카피/이벤트/비주얼 5분류
- **인사이트 추출** — 단순 변경 나열이 아닌, "왜 중요한가" 3~5줄

## 사전 준비물
- Notion DB "경쟁사" (브랜드명, 도메인, SNS 핸들)
- Notion DB "경쟁사 스냅샷 아카이브" (diff용)
- Firecrawl MCP 작동

→ [`실습.md`](실습.md)

---

## 실습 스킬

촬영·실습은 전용 스킬로 진행합니다. **"4-1 실습 시작"** 이라고 입력하면
[실습-4-1-competitor-monitor/SKILL.md](실습-4-1-competitor-monitor/SKILL.md) 의 게이트 흐름 (점검·설치 → 안내 → 데이터 준비 → 에이전트 열람 → 시연 → 산출물 확인) 이 시작됩니다.
샘플 데이터는 [실습-4-1-competitor-monitor/sample-data/](실습-4-1-competitor-monitor/sample-data/) 에 포함되어 있습니다.
