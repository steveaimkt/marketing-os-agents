# Part 6. 광고 성과 — 매체 3개·6개 분석 에이전트로 광고 운영 자동화

> 이 Part에서 배우는 것: Meta·Google·네이버 광고를 통합 모니터링하고, 임계치 위반 시 자동 알림 + 조치 제안.

## 6개 에이전트 + 1개 스킬

| # | 이름 | 역할 |
|---|---|---|
| 1 | **meta-ads-analyzer** | Meta 광고 성과 분석 → HTML + Notion |
| 2 | **google-ads-analyzer** | Google Ads 검색 성과 분석 |
| 3 | **naver-ads-analyzer** | 네이버 검색광고 분석 |
| 4 | **3media-integrated-reporter** | 3대 매체 통합 리포트 |
| 5 | **ad-performance-checker** | 임계치 자동 점검 + 알림 |
| 6 | **ab-test-analyzer** | A/B 결과 자동 해석 + 노션 라이브러리 |
| S | **html-report-template** | 광고·GA4 리포트 HTML 표준 스킬 |

## 핵심 안전 원칙

**광고비를 직접 움직이는 명령은 자동화 금지.**
- `ad-performance-checker`는 **읽기 전용**으로 점검만
- 임계치 위반 시 → 디스코드 #marketing-alerts 채널에 알림
- 조치(일시정지·예산 변경)는 사용자가 직접 또는 명시적 명령

## 임계치 표준 (기본값, 본 브랜드 데이터로 조정)

| 지표 | 경고 | 차단 |
|---|---|---|
| ROAS | < 2.0 | < 1.0 |
| CPA | > 30,000원 | > 50,000원 |
| CTR | < 1.0% | < 0.5% |
| 일일 광고비 초과 | > 110% | > 130% |

→ [`01-meta-ads-analyzer/`](01-meta-ads-analyzer/)
