# 클립 1-2. 에이전트 팀 역할 설계 — Part 1~9 통합 그림

## 30개 에이전트 매트릭스

```
                  ┌───────────────────┐
                  │  Orchestrator (1) │  ← 사용자가 보는 유일한 에이전트
                  └─────────┬─────────┘
                            │
   ┌────────────────────────┼────────────────────────┐
   ↓                        ↓                        ↓
[Research 5]          [Content 7]              [Analytics 9]
trend-scanner         email-newsletter         meta-ads-analyzer
competitor-monitor    content-publisher        google-ads-analyzer
ad-reference          brand-guidelines         naver-ads-analyzer
voc-analyzer          ad-copy-ab               3media-integrated
seo-keyword           landing-copy             ad-performance-checker
                      content-calendar         ab-test-analyzer
                      quality-reviewer-6axis   ga4-analyzer
                                               ga4-html-report
                                               ga4-notion-publisher
   ↓                        ↓                        ↓
[CRM 3]              [Strategy 3]             [Skills 5]
customer-unifier     marketing-calendar       newsletter-writing
cs-responder         claude-design            brand-voice
ltv-analyzer         strategy-report          ad-copy-ab
                                               quality-review-6axis
                                               html-report-template
```

## 데이터 흐름 (5단계)

```
[수집]   ← Firecrawl, GA4, Ads MCP들이 외부에서 가져옴
   ↓
[저장]   → Notion DB / Google Sheets (5개 카테고리)
   ↓
[가공]   ← 에이전트별 도메인 처리
   ↓
[합성]   ← 통합 에이전트 (3media, strategy-report)
   ↓
[발송]   → Discord / Gmail / Notion / Buffer
```

## 권한·트리거 표

| 에이전트 카테고리 | 트리거 | 권한 |
|---|---|---|
| Research (5) | 매일/매주 자동 + 명령 | 읽기 (Firecrawl·웹) |
| Content (7) | 명령 + 일정 | 읽기·쓰기 (Notion·Buffer) |
| Analytics (9) | 매주/매시간 자동 + 명령 | **읽기 전용** (광고비 보호) |
| CRM (3) | 월/주 자동 + 명령 | 읽기·쓰기 (시트·노션) |
| Strategy (3) | 분기/연간 + 명령 | 종합 |

→ [`실습.md`](실습.md)
