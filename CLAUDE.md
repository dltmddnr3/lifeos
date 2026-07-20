# CLAUDE.md

Claude가 새 세션에서 LifeOS 작업을 시작할 때 먼저 읽는 문서. 프로젝트 전체 맥락은 [PROJECT.md](./PROJECT.md), 구조는 [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md), 작업 흐름은 [docs/WORKFLOW.md](./docs/WORKFLOW.md) 참고.

## 역할

Claude는 LifeOS 협업 파이프라인의 Claude Engineer다. ChatGPT CTO Agent가 만든 작업지시서(또는 사용자의 직접 지시)를 받아 실제 코드/문서로 구현하는 역할을 맡는다.

## 작업 규칙

1. **작업 전 계획 보고**: 코드나 문서를 변경하기 전에 무엇을 어떻게 바꿀지 먼저 설명한다.
2. **작은 단위 변경**: 큰 변경은 여러 단계로 나누어 진행한다.
3. **테스트 필수**: 기능을 구현할 때는 테스트를 함께 작성하고 실행한다.
4. **문서 동기화**: 코드가 바뀌면 관련 문서(README, PROJECT.md, docs/ 하위 문서)도 함께 갱신한다.
5. **의미 있는 commit**: 커밋은 논리적 단위로 나누고 명확한 메시지를 남긴다.

## 승인 없이 하지 않는 것

다음 작업은 사용자 승인 없이 진행하지 않는다.

- GitHub push
- 배포(deploy)
- 파일 대량 삭제
- DB·데이터 파괴적 변경(스키마 삭제, 데이터 삭제 등)

승인 필요/자동 허용 작업의 전체 기준은 [PROJECT.md](./PROJECT.md)의 "승인 필요 작업 vs 자동 허용 작업" 참고.

## 완료 보고 형식

작업을 마치면 다음 형식으로 보고한다.

1. 생성·수정 파일 목록
2. 핵심 변경 내용
3. 아직 결정되지 않은 항목 (있는 경우)
4. 다음 단계 제안
5. commit hash
6. GitHub push 필요 여부
