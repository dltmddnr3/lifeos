# WORKFLOW

Slack `#lifeos` 채널을 기준으로 한 작업 처리 흐름. 전체 구조는 [ARCHITECTURE.md](./ARCHITECTURE.md), 역할 정의는 [../PROJECT.md](../PROJECT.md) 참고.

## 1. Slack 작업 요청 형식

- 채널: `#lifeos` (현재는 이 채널 하나만 사용, [DECISIONS.md](./DECISIONS.md) 참고)
- 형식: 정식 템플릿은 TBD. 현재는 자유 텍스트로 요구사항을 작성한다.
  - 예: "새 작업: 아이폰에서 오늘 할일을 볼 수 있게 해줘"
- 우선순위/기한 등 메타데이터 태그 형식은 TBD.

## 2. 작업 ID 생성

- LifeOS Manager가 요청을 감지하면 작업 ID를 발급한다. (형식 TBD, 예: `LIFEOS-0001`)
- 작업 ID를 기준으로 Slack 스레드를 생성하고, 이후 해당 작업의 모든 진행상황은 이 스레드에만 기록한다.

## 3. 요구사항 분석 (ChatGPT CTO Agent)

- LifeOS Manager가 요청 원문과 관련 문서(PROJECT.md, ARCHITECTURE.md 등)를 ChatGPT CTO Agent에 전달한다.
- ChatGPT CTO Agent는 PRD, 완료 조건, 작업 분해를 산출한다.

## 4. Claude 작업지시

- ChatGPT CTO Agent가 만든 작업지시서를 LifeOS Manager가 Claude Engineer에게 전달한다.
- 작업지시서에는 최소한 목표, 범위, 완료 조건, 제약사항이 포함되어야 한다.

## 5. 구현 (Claude Engineer)

- Claude Engineer는 작업 착수 전 변경 계획을 보고한다.
- 큰 변경은 작은 단위로 나누어 진행한다.
- [PROJECT.md](../PROJECT.md)의 "승인 필요 작업"에 해당하면 구현 전/중이라도 사용자 확인을 받는다.

## 6. 테스트

- 구현과 함께 테스트를 작성하고 실행한다.
- 테스트 결과는 결과 보고에 포함한다.

## 7. Commit

- 의미 있는 단위로 로컬 Git commit을 수행한다.
- 커밋 메시지 컨벤션은 TBD. 현재는 Conventional Commits 스타일(`docs:`, `feat:`, `fix:` 등)을 시범 사용한다.

## 8. Push

- 기본적으로 자동 push는 하지 않는다 (승인 필요 작업).
- 현재는 GitHub Desktop을 통한 수동 push만 사용한다.
- 자동 push 파이프라인 도입 여부는 이후 Phase에서 검토한다.

## 9. 결과 보고

- Claude Engineer는 [CLAUDE.md](../CLAUDE.md)의 완료 보고 형식에 따라 보고한다.
- LifeOS Manager는 보고 내용을 해당 작업의 Slack 스레드에 기록한다.

## 10. 승인 및 취소 흐름

- [PROJECT.md](../PROJECT.md)의 "승인 필요 작업"에 해당하는 항목은 LifeOS Manager가 스레드에서 사용자에게 명시적으로 승인을 요청한다.
- 사용자는 스레드에서 승인/거부/취소로 응답한다.
- 취소된 작업은 상태를 '취소'로 기록한다. 이미 진행된 변경사항을 되돌리는 절차는 TBD.
