# 클립 2-2. 자동 품질 검수 에이전트 — 6축 점수화

## 한 줄 요약
모든 카피를 **명확성·타겟·차별성·CTA·브랜드일관성·규제안전성** 6축으로 자동 점수.

## 에이전트 + 스킬
- [`agents/part5-copy/quality-reviewer-6axis.md`](../../../agents/part5-copy/quality-reviewer-6axis.md)
- [`skills/quality-review-6axis/SKILL.md`](../../../skills/quality-review-6axis/SKILL.md)

## 자동 차단 조건
- **규제 안전성 점수 ≤ 2** = `BLOCKED`, 자동 발송 보류
- 평균 < 3.5 = `REVISION_RECOMMENDED`, 재작성 1안 자동 생성

## 호출 흐름
다른 에이전트가 자동 호출:
- `ad-copy-ab` → 10패턴 모두 점수화
- `landing-copy` → 섹션별 점수화
- `email-newsletter` → 발송 전 본문 점수화
- `content-publisher` → 큐잉 전 채널별 점수화

→ [`실습.md`](실습.md)

---

## 실습 스킬

촬영·실습은 전용 스킬로 진행합니다. **"5-5 실습 시작"** 이라고 입력하면
[실습-5-5-quality-reviewer-6axis/SKILL.md](실습-5-5-quality-reviewer-6axis/SKILL.md) 의 게이트 흐름 (점검·설치 → 안내 → 데이터 준비 → 에이전트 열람 → 시연 → 산출물 확인) 이 시작됩니다.
샘플 데이터는 [실습-5-5-quality-reviewer-6axis/sample-data/](실습-5-5-quality-reviewer-6axis/sample-data/) 에 포함되어 있습니다.
