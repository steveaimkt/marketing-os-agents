# 클립 2-1. 고객 목소리(VoC) 분석 에이전트

## 한 줄 요약
**리뷰·댓글·CS 문의 500건을 매주 자동 분류**하고, 클러스터링해서 페인 포인트 TOP 5를 추출. 1주에 1시간 절약.

## 에이전트
[`agents/part4-research/voc-analyzer.md`](../../../agents/part4-research/voc-analyzer.md)

## 분류 모델 (5축)
1. 감정 점수 (-2 ~ +2)
2. 카테고리 (제품·디자인·배송·CS·가격)
3. 긴급도 (0~3)
4. 신규성 (이전 주에 안 나온 표현?)
5. 영향도 (해결 시 매출 영향)

## 다른 에이전트와의 연결
- Part 5 `landing-copy`가 페인 포인트를 카피에 반영
- Part 8 `cs-responder`가 자주 묻는 질문 학습

→ [`실습.md`](실습.md)

---

## 실습 스킬

촬영·실습은 전용 스킬로 진행합니다. **"4-4 실습 시작"** 이라고 입력하면
[실습-4-4-voc-analyzer/SKILL.md](실습-4-4-voc-analyzer/SKILL.md) 의 게이트 흐름 (점검·설치 → 안내 → 데이터 준비 → 에이전트 열람 → 시연 → 산출물 확인) 이 시작됩니다.
샘플 데이터는 [실습-4-4-voc-analyzer/sample-data/](실습-4-4-voc-analyzer/sample-data/) 에 포함되어 있습니다.
