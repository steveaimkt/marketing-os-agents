# 클립 1-3. GA4 + Notion 발송 에이전트

[`agents/part7-ga4/ga4-notion-publisher.md`](../../../agents/part7-ga4/ga4-notion-publisher.md)

HTML → 노션 페이지 변환 + 디스코드 첨부 + (선택) 사내 메일 발송.

## 실습
```bash
claude --agent ga4-notion-publisher "이번 주 리포트 발송"
```

## Part 7 종료 체크리스트
- [ ] 3개 에이전트 차례로 실행 성공
- [ ] 디스코드에서 HTML 첨부 미리보기 확인
- [ ] 노션 페이지 자동 생성 확인
- [ ] (Part 10 미리보기) 3개를 한 번에 호출하는 시나리오 이해

→ Part 8 [`../../part08-CRM리텐션/README.md`](../../part08-CRM리텐션/README.md)
