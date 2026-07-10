# 클립 1-3. 마케팅 전략 보고서 자동 생성

[`agents/part9-expansion/strategy-report-generator.md`](../../../agents/part9-expansion/strategy-report-generator.md)

분기·연말 임원 보고서를 6개 에이전트 데이터를 종합해 **30페이지 + 1페이지 요약** 자동 생성.

## 5장 구조
1. Executive Summary (1p)
2. 마케팅 성과 (10p)
3. 고객 인사이트 (8p)
4. 경쟁 환경 (5p)
5. 다음 분기 전략 (6p)

→ [`실습.md`](실습.md)

---

## 실습 스킬

이 실습도 9-2 와 같은 핸드오프 패턴입니다 — **클로드코드=집계·기획 / 클로드 디자인=시각 리포트**. 클로드코드가 5~6개 분석 에이전트를 병렬 집계해 5장 `report-content.md` + 임원 1p 디자인 프롬프트를 만들고, 그 프롬프트를 **클로드 디자인(claude.ai Artifacts)** 에 넘겨 임원용 시각 리포트를 생성합니다.

촬영·실습은 전용 스킬로 진행합니다. **"9-3 실습 시작"** 이라고 입력하면
[실습-9-3-strategy-report-generator/SKILL.md](실습-9-3-strategy-report-generator/SKILL.md) 의 게이트 흐름 (점검 → 역할 분리 안내 → 5~6 집계 → report-content.md + 프롬프트 산출 → 클로드 디자인 핸드오프 → 발행) 이 시작됩니다.
폴백 픽스처(선행 5~6개 에이전트 요약)·디자인 프롬프트 골격·결과 레퍼런스는 [실습-9-3-strategy-report-generator/sample-data/](실습-9-3-strategy-report-generator/sample-data/) 에 포함되어 있습니다.
