# cavecrew

결정 가이드. 인라인 작업 대신 케이브맨 서브에이전트에 위임할 때.

## 기능

케이브맨 스타일 서브에이전트와 바닐라 대안 중 언제 스폰할지 메인 스레드에게 알려줌. 핵심 이점: 서브에이전트 도구 결과가 메인 컨텍스트에 그대로 주입되는데, 케이브맨 출력은 바닐라 산문의 약 1/3 크기. 한 세션에서 20번 위임하면 컨텍스트 소진과 작업 완료의 차이가 날 수 있음.

서브에이전트 3종:

| 서브에이전트 | 역할 | 사용 시점 |
|------------|------|----------|
| `cavecrew-investigator` | 코드 위치 파악 (읽기 전용) | "X가 어디 정의됐나 / Y를 뭐가 호출하나 / Z 사용처 목록" |
| `cavecrew-builder` | 외과적 편집, 1-2 파일 | 범위 명확, ≤2 파일. 3파일 이상 거부. |
| `cavecrew-reviewer` | diff/파일 리뷰 | 심각도 이모지 있는 한 줄 발견 사항 |

산문, 아키텍처 해설, 근거를 원할 때는 바닐라 `Explore` 또는 `Code Reviewer`. 한 줄 답변과 3파일 이상 리팩터는 메인 스레드 직접 처리.

이 스킬은 결정 가이드, 슬래시 명령어 아님. 대화에서 위임 언급 시 활성화.

## 호출 방법

"서브에이전트에 위임", "cavecrew 사용", "investigator 스폰", "컨텍스트 절약", "압축된 에이전트 출력" 같은 구문에 트리거.

## 연쇄 예시

위치 → 수정 → 검증 (가장 일반적):

1. `cavecrew-investigator`가 사이트 목록 반환 (`path:line — symbol — note`)
2. 메인 스레드가 1-2 사이트 선택, `cavecrew-builder`에 경로 전달
3. `cavecrew-reviewer`가 결과 diff 감사

병렬 탐색: 다른 각도(정의, 호출자, 테스트)로 `cavecrew-investigator` 2-3개를 한 메시지에 스폰. 메인에서 집계.

## 참고

- [`SKILL.md`](./SKILL.md) — 전체 결정 매트릭스 및 출력 계약
- [`agents/cavecrew-investigator.md`](../../agents/cavecrew-investigator.md)
- [`agents/cavecrew-builder.md`](../../agents/cavecrew-builder.md)
- [`agents/cavecrew-reviewer.md`](../../agents/cavecrew-reviewer.md)
- [Caveman README](../../README.md) — 저장소 개요
