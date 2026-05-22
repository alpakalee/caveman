# caveman-stats

실제 세션 토큰 영수증. AI 추정치 없음.

## 기능

현재 Claude Code 세션 로그를 직접 읽어 실제 입/출력 토큰 사용량과 non-caveman 기준 대비 예상 절감량 보고. 수치는 디스크의 JSONL 세션 로그에서 — 모델이 직접 계산하거나 추정하지 않음. 출력은 `caveman-mode-tracker` hook이 주입, `/caveman-stats`를 가로채 포맷된 통계를 차단 결정 이유로 반환.

매 실행 시 상태 표시줄 배지(`⛏ 12.4k`)가 사용하는 라이프타임 절감량 접미사 파일도 기록.

## 호출 방법

```
/caveman-stats
```

## 출력 예시

```
세션: 47턴
입력:   12,304 토큰
출력:    3,891 토큰 (caveman)
기준선: 11,247 토큰 (caveman 없이 추정)
절감:    7,356 토큰 (~65%)
```

## 참고

- [`SKILL.md`](./SKILL.md) — hook 계약 및 메커니즘
- [Caveman README](../../README.md) — 저장소 개요
