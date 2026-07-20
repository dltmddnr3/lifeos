# PROJECT

## 비전

아이폰만으로 모든 개발과 운영이 가능한 AI 시스템(LifeOS)을 만든다. 사용자는 Slack에 요구사항만 남기면, ChatGPT CTO Agent가 설계하고 Claude Engineer가 구현하며, LifeOS Manager가 전체 파이프라인을 조율한다. 사용자는 터미널이나 IDE를 열지 않고도 개발 전 과정을 요청·승인·확인할 수 있어야 한다.

## 핵심 운영 원칙

### 아이폰 중심 운영 원칙

- 요청, 승인, 진행상황 확인은 모두 아이폰의 Slack 앱에서 가능해야 한다.
- Mac mini는 실행 인프라(compute)일 뿐이며, 사용자가 직접 조작할 필요를 최소화한다.

### 터미널 최소화 원칙

- 사용자는 원칙적으로 터미널을 직접 열 필요가 없다.
- 명령 실행은 Claude Engineer 또는 LifeOS Manager가 대행한다.
- 불가피하게 GUI가 필요한 경우 GitHub Desktop 같은 GUI 도구를 우선 사용한다.

## 역할

| 역할 | 담당 | 책임 |
|---|---|---|
| Product Owner | 사용자 | Slack에서 요구사항 입력, 주요 변경 승인 |
| CTO Agent | ChatGPT | 요구사항 분석, PRD·아키텍처 설계, 작업 분해, 완료 조건 정의, Claude 작업지시서 생성, 구현 결과 검수 |
| Engineer | Claude | 코드 구현, 테스트, 문서 업데이트, 로컬 Git commit, 실행 결과 보고 |
| Manager | LifeOS Manager | Slack 메시지 수신, 작업 ID·상태 관리, ChatGPT CTO Agent 호출, Claude 실행 요청, 진행 상황을 Slack 스레드에 기록, 승인·취소 처리, 결과와 commit 기록 |

역할별 상세 흐름은 [docs/WORKFLOW.md](./docs/WORKFLOW.md), 전체 구조는 [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md) 참고.

## 현재 Phase와 로드맵

**Phase 0 (현재) — 협업 기반.** 사용자·ChatGPT CTO Agent·Claude Engineer·LifeOS Manager가 Slack에서 협업하는 파이프라인의 기준 문서를 정의하는 단계. 코드 구현은 아직 시작하지 않았다.

전체 로드맵(Phase 0~6)은 [docs/ROADMAP.md](./docs/ROADMAP.md) 참고.

## 승인 필요 작업 vs 자동 허용 작업

**승인 필요 (사용자 확인 전에는 진행하지 않음)**

- GitHub push
- 배포(deploy)
- 파일 대량 삭제
- DB·데이터 파괴적 변경(스키마 삭제, 데이터 삭제 등)
- 주요 아키텍처/기술 스택 결정
- 새 외부 서비스·API 연동 추가

**자동 허용 (Claude Engineer가 바로 진행 가능)**

- 로컬 코드 작성·수정
- 로컬 Git commit
- 문서 업데이트
- 테스트 작성 및 실행
- 비파괴적 리팩토링

## 환경 노트

- 개발 위치: Mac mini, 경로 `~/developer/lifeos`
- Claude Engineer(Cowork)의 명령 실행 환경은 격리된 Linux 샌드박스이며, 연결된 프로젝트 폴더만 마운트되어 파일이 실제 Mac에 반영된다. Xcode 등 macOS 전용 도구는 이 샌드박스에서 사용할 수 없다.
- 샌드박스의 외부 네트워크 접근이 기본 차단되어 있어 GitHub push/clone은 현재 불가능. 초기에는 GitHub Desktop으로 수동 push한다. 자세한 내용은 [docs/DECISIONS.md](./docs/DECISIONS.md) 참고.
- LifeOS Manager를 포함한 협업 파이프라인의 세부 기술 선택은 아직 미정(TBD). [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md)의 "아직 미정인 기술 선택" 참고.

## 변경 이력

- 2026-07-20: Phase 0 시작. 프로젝트 골격(README, PROJECT.md, docs/scripts/src/tests) 생성.
- 2026-07-20: 협업 파이프라인(사용자/ChatGPT CTO/Claude Engineer/LifeOS Manager) 기준 문서 체계 정의. PROJECT.md 개편, ARCHITECTURE·WORKFLOW·ROADMAP·DECISIONS·CLAUDE.md 추가.
