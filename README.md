# LifeOS

아이폰만으로 모든 개발과 운영이 가능한 AI 시스템을 만드는 프로젝트.

## 현재 상태

**Phase 0 — 개발 환경 구축.** 기술 스택은 아직 확정되지 않았다. ChatGPT(CTO)와의 설계가 끝나는 대로 실제 코드가 채워진다.

## 폴더 구조

```
lifeos/
├── README.md      이 파일
├── PROJECT.md      역할, 원칙, Phase 로드맵
├── docs/           설계 문서, 의사결정 기록
├── scripts/        개발/운영 자동화 스크립트
├── src/            애플리케이션 코드 (스택 확정 후 채워짐)
├── tests/          테스트 코드
└── .gitignore
```

## 역할

- **ChatGPT (CTO)**: 설계·아키텍처 결정
- **Claude (Lead Software Engineer)**: 설계를 실제 코드로 구현, 테스트, 커밋/푸시, 리팩토링
- **사용자**: 방향 설정, 최종 승인

자세한 협업 원칙은 [PROJECT.md](./PROJECT.md) 참고.
