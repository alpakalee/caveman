# caveman-review

한 줄 PR 코멘트. 위치, 문제, 수정. 서론 없음.

## 기능

`L<줄>: <심각도> <문제>. <수정>.` 형식으로 코드 리뷰 코멘트 생성. 발견 사항당 한 줄. 심각도 이모지: 🔴 bug, 🟡 risk, 🔵 nit, ❓ question. "I noticed that...", 헤징, diff가 이미 보여주는 내용 반복 제거. 정확한 줄 번호, 백틱 기호, 구체적 수정 유지.

자동 명확화: CVE급 보안 발견, 아키텍처 이견, 작성자가 *왜*를 알아야 하는 온보딩 컨텍스트에서는 간결 모드 해제. 나머지는 간결 재개.

출력만 — 승인, 변경 요청, 린터 실행 안 함.

## 호출 방법

```
/caveman-review
```

"이 PR 리뷰", "코드 리뷰", "diff 리뷰"에도 트리거.

## 출력 예시

```
L42: 🔴 bug: user can be null after .find(). Add guard before .email.
L88-140: 🔵 nit: 50-line fn does 4 things. Extract validate/normalize/persist.
L23: 🟡 risk: no retry on 429. Wrap in withBackoff(3).
L107: ❓ q: why drop the cache here? Reads on next request will miss.
```

## 참고

- [`SKILL.md`](./SKILL.md) — 전체 LLM 지시 사항
- [Caveman README](../../README.md) — 저장소 개요
