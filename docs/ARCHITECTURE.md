# ARCHITECTURE

## 전체 구조

```
사용자 (iPhone Slack)
      │  요구사항 입력 / 승인 / 취소
      ▼
   #lifeos 채널
      │
      ▼
 LifeOS Manager  ──────────────► GitHub (백업/복구)
      │        ▲
      │ 작업지시 │ 결과 보고
      ▼        │
 ChatGPT CTO Agent      Claude Engineer
 (PRD/설계/작업분해)      (구현/테스트/로컬 commit)
```

LifeOS Manager가 중앙 오케스트레이터 역할을 하며, Slack ↔ ChatGPT CTO Agent ↔ Claude Engineer ↔ GitHub 사이의 모든 호출과 기록을 중개한다.

## 컴포넌트 책임

- **Slack (#lifeos)**: 사용자와 시스템 사이의 유일한 인터페이스. 작업 요청, 진행상황 확인, 승인/취소가 모두 여기서 이루어진다.
- **LifeOS Manager**: 메시지 수신, 작업 ID·상태 관리, ChatGPT/Claude 호출 라우팅, Slack 스레드 기록, 승인·취소 처리. 구현 방식은 TBD (아래 "미정인 기술 선택" 참고).
- **ChatGPT CTO Agent**: 요구사항 분석, PRD·아키텍처 설계, 작업 분해, 완료 조건 정의, Claude 작업지시서 생성, 구현 결과 검수.
- **Claude Engineer**: 작업지시서 기반 코드 구현, 테스트, 문서 업데이트, 로컬 Git commit, 실행 결과 보고. (현재는 Mac mini의 Claude Desktop/Cowork 세션으로 동작)
- **GitHub**: 소스 코드 백업과 복구용 원격 저장소. 초기에는 GitHub Desktop을 통한 수동 push.
- **Mac mini**: LifeOS Manager와 Claude Engineer가 실행되는 인프라. 사용자가 직접 조작하는 대상이 아니다.

## 메시지 흐름

1. 사용자가 `#lifeos`에 요구사항을 작성한다.
2. LifeOS Manager가 메시지를 감지하고 작업 ID를 발급, 해당 작업 전용 Slack 스레드를 생성한다.
3. LifeOS Manager가 요구사항과 관련 문서(PROJECT.md 등)를 ChatGPT CTO Agent에 전달한다.
4. ChatGPT CTO Agent가 PRD, 작업 분해, 완료 조건, Claude 작업지시서를 반환한다.
5. LifeOS Manager가 결과를 스레드에 기록하고, 필요 시(PROJECT.md의 "승인 필요 작업") 사용자 승인을 요청한다.
6. 승인되면 LifeOS Manager가 Claude Engineer에게 작업지시서를 전달해 실행을 요청한다.
7. Claude Engineer가 구현·테스트·로컬 commit 후 결과를 보고한다.
8. LifeOS Manager가 결과와 commit 기록을 스레드에 남기고, GitHub push 필요 여부를 안내한다.
9. 사용자가 push를 승인하면 (현재는) GitHub Desktop으로 수동 반영한다.

## 데이터 흐름

- **작업 상태**: 작업 ID, 상태(요청 → 분석중 → 승인대기 → 구현중 → 완료/취소), 관련 커밋 해시. 저장 방식(파일 기반 JSON, SQLite, 기타 DB 등)은 TBD.
- **의사결정/대화 로그**: Slack 스레드가 1차 기록, `docs/DECISIONS.md`가 주요 결정의 2차 기록.
- **코드/문서**: Git 저장소가 단일 소스(source of truth).

## 장애 발생 시 처리 방향

- **ChatGPT 호출 실패**: LifeOS Manager가 제한적으로 재시도하고, 실패 시 Slack 스레드에 오류를 보고한 뒤 사용자 개입을 기다린다.
- **Claude 실행 실패/중단**: 부분 결과와 오류 내용을 스레드에 기록한다. 자동 재시도는 하지 않는다(파괴적 작업 가능성). 사용자 확인 후 재시작.
- **GitHub push 실패**: 로컬 commit은 그대로 유지하고 실패 사실만 보고한다. 자동 재시도하지 않는다.
- **외부 API(Slack/ChatGPT 등) 네트워크 단절**: 이 상황을 로컬에 큐잉할지, 단순 실패 처리할지는 TBD.

## 아직 미정인 기술 선택

- LifeOS Manager 구현 언어/런타임: TBD
- LifeOS Manager 실행 위치 (Mac mini 상시 프로세스 vs 서버리스 vs 기타): TBD
- 작업 상태 저장소 (JSON 파일 vs SQLite vs 기타 DB): TBD
- Slack 연동 방식 (Slack Bot API vs Slack MCP 등): TBD
- ChatGPT 연동 방식 (OpenAI API 직접 호출 vs Assistants API vs 기타): TBD
- Claude 실행 트리거 방식 (현재는 Cowork 세션 수동 실행 vs 향후 API 자동화): TBD
- 인증/보안 (토큰 저장 위치, 권한 범위, 시크릿 관리): TBD
