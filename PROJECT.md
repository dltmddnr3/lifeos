# PROJECT

## 비전

아이폰만으로 모든 개발과 운영이 가능한 AI 시스템을 만든다. 사용자(체리)는 Slack에 요구사항만 남기면, 베리(ChatGPT, CTO)가 설계하고 망고(Claude, Lead Engineer)가 구현하며, 매니저가 전체 파이프라인을 조율한다. 사용자는 터미널이나 IDE를 열지 않고도 개발 전 과정을 요청·승인·확인할 수 있어야 한다.

CherryBox는 이 비전을 실현하기 위해 만들어진 협업 AI 회사다. 이 저장소는 CherryBox의 협업 모델·역할·워크플로우·거버넌스를 정의하는 회사 운영 문서를 담는다. CherryBox가 만드는 개별 제품은 [products/](./products/)에 간단히 기록하고, 실제 구현은 제품별 별도 저장소(예: [turn-on](../turn-on))에서 진행한다.

## 핵심 운영 원칙

### 아이폰 중심 운영 원칙

- 요청, 승인, 진행상황 확인은 모두 아이폰의 Slack 앱에서 가능해야 한다.
- Mac mini는 실행 인프라(compute)일 뿐이며, 사용자가 직접 조작할 필요를 최소화한다.

### 터미널 최소화 원칙

- 사용자는 원칙적으로 터미널을 직접 열 필요가 없다.
- 명령 실행은 망고(Claude Engineer) 또는 매니저가 대행한다.
- 불가피하게 GUI가 필요한 경우 GitHub Desktop 같은 GUI 도구를 우선 사용한다.

## 역할

CherryBox의 역할과 담당자는 [roles/](./roles/)에 개별 문서로 정리되어 있다.

| 역할 | 담당 |
|---|---|
| Founder / Product Owner | [체리](./roles/founder.md) (사용자) |
| CTO Agent | [베리](./roles/cto.md) (ChatGPT) |
| Lead Engineer | [망고](./roles/engineer.md) (Claude) |
| Manager | [매니저](./roles/manager.md) (담당 미정, 오케스트레이터 역할) |

역할별 상세 흐름은 [workflows/task-workflow.md](./workflows/task-workflow.md), 전체 구조는 [workflows/architecture.md](./workflows/architecture.md) 참고.

## 현재 Phase와 로드맵

**Phase 0 (현재) — 협업 기반.** 체리·베리·망고·매니저가 Slack에서 협업하는 파이프라인의 기준 문서를 정의하는 단계. 회사 문서 정의 후 첫 제품인 Turn On의 구현을 시작한다.

전체 로드맵(Phase 0~6)은 [ROADMAP.md](./ROADMAP.md) 참고.

## 승인 필요 작업 vs 자동 허용 작업

**승인 필요 (사용자 확인 전에는 진행하지 않음)**

- GitHub push
- 배포(deploy)
- 파일 대량 삭제
- DB·데이터 파괴적 변경(스키마 삭제, 데이터 삭제 등)
- 주요 아키텍처/기술 스택 결정
- 새 외부 서비스·API 연동 추가

**자동 허용 (망고/Claude Engineer가 바로 진행 가능)**

- 로컬 코드 작성·수정
- 로컬 Git commit
- 문서 업데이트
- 테스트 작성 및 실행
- 비파괴적 리팩토링

## 환경 노트

- 개발 위치: Mac mini, 경로 `~/developer/lifeos` (CherryBox 회사 저장소)
- Claude Engineer(Cowork)의 명령 실행 환경은 격리된 Linux 샌드박스이며, 연결된 프로젝트 폴더만 마운트되어 파일이 실제 Mac에 반영된다. Xcode 등 macOS 전용 도구는 이 샌드박스에서 사용할 수 없다.
- 샌드박스의 외부 네트워크 접근이 기본 차단되어 있어 GitHub push/clone은 현재 불가능. 초기에는 GitHub Desktop으로 수동 push한다. 자세한 내용은 [decisions/DECISIONS.md](./decisions/DECISIONS.md) 참고.
- 매니저를 포함한 협업 파이프라인의 세부 기술 선택은 아직 미정(TBD). [workflows/architecture.md](./workflows/architecture.md)의 "아직 미정인 기술 선택" 참고.

## 변경 이력

- 2026-07-20: Phase 0 시작. 프로젝트 골격(README, PROJECT.md, docs/scripts/src/tests) 생성.
- 2026-07-20: 협업 파이프라인(사용자/ChatGPT CTO/Claude Engineer/LifeOS Manager) 기준 문서 체계 정의. PROJECT.md 개편, ARCHITECTURE·WORKFLOW·ROADMAP·DECISIONS·CLAUDE.md 추가.
- 2026-07-20: 회사명을 CherryBox로 정리하고 저장소를 회사 운영 문서 구조(roles/workflows/memory/decisions/products)로 재편. 역할에 체리/베리/망고 명칭 부여. 첫 제품 Turn On을 별도 저장소로 분리하고 products/turn-on.md에 기록.
