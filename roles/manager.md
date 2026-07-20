# 매니저 — Manager (담당 미정)

**담당**: 미정. 현재는 사람(체리)이 Slack ↔ 베리 ↔ 망고 사이를 수동으로 중개하고 있으며, 향후 이 역할을 대행하는 컴포넌트(오케스트레이터)를 만들 계획이다.

**책임**:
- Slack 메시지 수신
- 작업 ID·상태 관리
- 베리(ChatGPT CTO Agent) 호출
- 망고(Claude Engineer) 실행 요청
- 진행 상황을 Slack 스레드에 기록
- 승인·취소 처리
- 결과와 commit 기록 정리

구현 언어/런타임, 실행 위치, 상태 저장소 등 매니저의 기술 선택은 아직 미정이다. 자세한 내용은 [../workflows/architecture.md](../workflows/architecture.md)의 "아직 미정인 기술 선택" 참고.
