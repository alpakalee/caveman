---
name: caveman-stats
description: >
  현재 세션의 실제 토큰 사용량과 예상 절감량 표시.
  Claude Code 세션 로그에서 직접 읽음 — AI 추정치 아님.
  /caveman-stats 트리거. 출력은 mode-tracker hook이 주입; 모델이 수치 계산 안 함.
---

This skill is delivered by `hooks/caveman-stats.js` (read by `hooks/caveman-mode-tracker.js` on `/caveman-stats`). The model does not need to do anything when this skill fires — the hook returns `decision: "block"` with the formatted stats as the reason. The user sees the numbers immediately.
