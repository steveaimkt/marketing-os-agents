# 클립 2-1. 광고 성과 체크 에이전트 — 24시간 워치독

[`agents/part6-ads/ad-performance-checker.md`](../../../agents/part6-ads/ad-performance-checker.md)

**매시간 자동 점검**. ROAS·CPA·CTR·예산 임계치 위반 시에만 디스코드 #marketing-alerts 알림.

## 핵심 디자인
- **위반 없으면 침묵** — 알림 스팸 방지
- **3시간 연속 위반 = Critical** (📢 mention)
- **자동 일시정지 없음** — reaction 승인 후만 실행 (Part 10에서 Hook 연결)

→ [`실습.md`](실습.md)

---

## 실습 스킬

촬영·실습은 전용 스킬로 진행합니다. **"6-5 실습 시작"** 이라고 입력하면
[실습-6-5-ad-performance-checker/SKILL.md](실습-6-5-ad-performance-checker/SKILL.md) 의 게이트 흐름 (점검·설치 → 안내 → 데이터 준비 → 에이전트 열람 → 시연 → 산출물 확인) 이 시작됩니다.
샘플 데이터는 [실습-6-5-ad-performance-checker/sample-data/](실습-6-5-ad-performance-checker/sample-data/) 에 포함되어 있습니다.
