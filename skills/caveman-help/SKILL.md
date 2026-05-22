---
name: caveman-help
description: >
  모든 caveman 모드, 스킬, 명령어 빠른 참조 카드.
  일회성 표시, 지속 모드 아님.
  트리거: /caveman-help, "caveman 도움말", "caveman 명령어", "caveman 어떻게 써".
---

# Caveman 도움말

호출 시 이 참조 카드 표시. 일회성 — 모드 변경, 플래그 파일 쓰기, 영속화 금지. 케이브맨 스타일로 출력.

## 모드

| 모드 | 트리거 | 변경 내용 |
|------|--------|----------|
| **Lite** | `/caveman lite` | 필러 제거. 문장 구조 유지. |
| **Full** | `/caveman` | 관사, 필러, 인사말, 헤징 제거. 단편 OK. 기본값. |
| **Ultra** | `/caveman ultra` | 극단적 압축. 나체 단편. 산문 대신 표. |
| **Wenyan-Lite** | `/caveman wenyan-lite` | 고전 중국어 스타일, 가벼운 압축. |
| **Wenyan-Full** | `/caveman wenyan` | 완전 文言文. 최대 고전 간결함. |
| **Wenyan-Ultra** | `/caveman wenyan-ultra` | 극단적. 예산 압박받는 고대 학자. |

모드는 변경하거나 세션 종료 시까지 유지.

## 스킬

| 스킬 | 트리거 | 기능 |
|------|--------|------|
| **caveman-commit** | `/caveman-commit` | 간결한 커밋 메시지. Conventional Commits. 제목 ≤50자. |
| **caveman-review** | `/caveman-review` | 한 줄 PR 코멘트: `L42: bug: user null. Add guard.` |
| **caveman-compress** | `/caveman-compress <파일>` | .md 파일을 케이브맨 산문으로 압축. 입력 토큰 ~46% 절감. |
| **caveman-help** | `/caveman-help` | 이 카드. |

## 비활성화

"stop caveman" 또는 "normal mode". 언제든 `/caveman`으로 재개.

## 기본 모드 설정

기본 모드 = `full`. 변경 방법:

**환경 변수** (최우선):
```bash
export CAVEMAN_DEFAULT_MODE=ultra
```

**설정 파일** (`~/.config/caveman/config.json`):
```json
{ "defaultMode": "lite" }
```

`"off"` 설정 시 세션 시작 시 자동 활성화 비활성화. 사용자는 `/caveman`으로 수동 활성화 가능.

우선순위: 환경 변수 > 설정 파일 > `full`.

## 더보기

전체 문서: https://github.com/alpakalee/caveman
