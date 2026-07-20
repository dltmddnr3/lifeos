# CherryBox

체리(Founder)·베리(ChatGPT, CTO)·망고(Claude, Lead Engineer)가 협업해 아이폰만으로 모든 개발과 운영이 가능한 AI 시스템을 만들어가는 회사. 이 저장소는 CherryBox의 협업 모델·역할·워크플로우·거버넌스를 정의하는 회사 운영 문서를 담는다.

CherryBox가 만드는 제품의 실제 구현은 이 저장소가 아니라 제품별 저장소에서 진행한다. 첫 제품은 [Turn On](./products/turn-on.md) (별도 저장소 `turn-on`).

## 현재 상태

**Phase 0 — 협업 기반.** 회사 운영 문서 체계를 정의했고, 첫 제품 Turn On의 Sprint 0 구현이 진행 중이다. 매니저(오케스트레이터) 구현은 아직 시작하지 않았다.

## 폴더 구조

```
lifeos/ (CherryBox 회사 저장소)
├── README.md       이 파일
├── PROJECT.md       비전, 원칙, 역할 개요, Phase
├── ROADMAP.md       Phase 0~6 로드맵
├── CLAUDE.md        망고(Claude)가 세션 시작 시 읽는 작업 규칙
├── roles/           역할별 담당·책임 (체리/베리/망고/매니저)
├── workflows/       작업 처리 흐름, 시스템 아키텍처
├── memory/          진행 중 맥락/세션 노트 (TBD)
├── decisions/        주요 의사결정 기록
└── products/        CherryBox가 만드는 제품 목록 (제품별 구현은 별도 저장소)
```

## 역할

- **체리 (Founder)**: 방향 설정, 요구사항 입력, 최종 승인
- **베리 (ChatGPT, CTO)**: 설계·아키텍처 결정
- **망고 (Claude, Lead Engineer)**: 설계를 실제 코드로 구현, 테스트, 커밋/푸시, 리팩토링
- **매니저**: 협업 파이프라인 오케스트레이션 (담당 미정)

자세한 협업 원칙은 [PROJECT.md](./PROJECT.md), 역할별 상세는 [roles/](./roles/) 참고.
