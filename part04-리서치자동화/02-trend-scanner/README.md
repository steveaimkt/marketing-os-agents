# 클립 1-2. 트렌드 스캔 에이전트

## 한 줄 요약
**네이버·구글·X·인스타** 트렌드를 매일 자동 수집해 노션 "주간 트렌드" DB에 적재. `email-newsletter`의 입력이 됨.

## 에이전트
[`agents/part4-research/trend-scanner.md`](../../../agents/part4-research/trend-scanner.md)

## 핵심 디자인
- **관련성 점수 (0~5)** — 본 카테고리와 무관한 키워드는 자동 필터
- **급상승 감지** — 출현 빈도 + 신규성으로 TOP 3 알림
- **다른 에이전트의 입력** — `email-newsletter`가 이 DB를 매주 월요일 읽음

→ [`실습.md`](실습.md)

---

## 실습 스킬

촬영·실습은 전용 스킬로 진행합니다. **"4-2 실습 시작"** 이라고 입력하면
[실습-4-2-trend-scanner/SKILL.md](실습-4-2-trend-scanner/SKILL.md) 의 게이트 흐름 (점검·설치 → 안내 → 데이터 준비 → 에이전트 열람 → 시연 → 산출물 확인) 이 시작됩니다.
샘플 데이터는 [실습-4-2-trend-scanner/sample-data/](실습-4-2-trend-scanner/sample-data/) 에 포함되어 있습니다.
