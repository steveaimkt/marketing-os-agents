# Part 7. 데이터 분석 — GA4부터 통합 대시보드까지

> 이 Part에서 배우는 것: GA4 데이터를 매주 자동 분석·시각화·발송하는 3개 에이전트 체이닝.

## 3개 에이전트 (순차 호출)

```
[ga4-analyzer] → 데이터 추출·시트 정리
    ↓
[ga4-html-report] → HTML 시각화
    ↓
[ga4-notion-publisher] → 노션 발송 + 디스코드
```

| # | 이름 | 입력 | 출력 |
|---|---|---|---|
| 1 | **ga4-analyzer** | GA4 속성 ID, 기간 | Google Sheets에 채널·페이지·전환 표 |
| 2 | **ga4-html-report** | Sheets 결과 | 단일 HTML 파일 (Chart.js 인라인) |
| 3 | **ga4-notion-publisher** | HTML 파일 | 노션 페이지 + 디스코드 첨부 발송 |

→ [`01-ga4-analyzer/`](01-ga4-analyzer/)
