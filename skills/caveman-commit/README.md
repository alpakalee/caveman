# caveman-commit

간결한 Conventional Commits. 무엇보다 왜.

## 기능

Conventional Commits 형식으로 커밋 메시지 생성. 제목 ≤50자, 하드 캡 72자. 명령형. 본문은 *왜*가 불명확하거나 breaking change가 있을 때만. AI 귀속 없음, "this commit does X" 없음, 프로젝트 관례 없으면 이모지 없음. breaking change, 보안 수정, 데이터 마이그레이션, revert에는 본문 항상 필요 — 미래 디버거에게 컨텍스트 필요.

메시지만 출력. stage, commit, amend 안 함.

## 호출 방법

```
/caveman-commit
```

"커밋 작성", "커밋 메시지", "커밋 생성" 같은 구문에도 트리거.

## 출력 예시

diff: 사용자 프로필 신규 엔드포인트.

```
feat(api): add GET /users/:id/profile

Mobile client needs profile data without the full user payload
to reduce LTE bandwidth on cold-launch screens.

Closes #128
```

diff: breaking API 이름 변경.

```
feat(api)!: rename /v1/orders to /v1/checkout

BREAKING CHANGE: clients on /v1/orders must migrate to /v1/checkout
before 2026-06-01. Old route returns 410 after that date.
```

## 참고

- [`SKILL.md`](./SKILL.md) — 전체 LLM 지시 사항
- [Caveman README](../../README.md) — 저장소 개요
