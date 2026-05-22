# caveman

스마트 케이브맨처럼 말해. 같은 뇌, 더 적은 토큰.

## 기능

모든 모델 응답을 케이브맨 스타일 산문으로 압축. 관사, 필러, 인사말, 헤징 제거. 모든 기술적 세부 사항, 코드 블록, 오류 문자열, 기호는 정확하게 유지. 출력 토큰 ~65-75% 절감, 완전한 정확도 보존. 모드는 변경하거나 중지할 때까지 세션 전체 유지.

강도 레벨 6단계:

| 레벨 | 변경 내용 |
|------|----------|
| `lite` | 필러/헤징 제거. 문장 완전 유지. 전문적이지만 간결. |
| `full` | 기본값. 관사 제거, 단편 OK, 짧은 동의어. |
| `ultra` | 나체 단편. 약어(DB, auth, fn). 인과관계에 화살표. |
| `wenyan-lite` | 고전 중국어 어투, 가벼운 압축. |
| `wenyan-full` | 최대 文言文. 80-90% 글자 감소. |
| `wenyan-ultra` | 극단적 고전 압축. |

자동 명확화 규칙: 보안 경고, 비가역적 작업 확인, 단편 모호성이 오독 위험이 있는 다단계 시퀀스, 사용자가 질문 반복 시 케이브맨을 일반 산문으로 전환. 명확한 부분 후 재개.

## 호출 방법

```
/caveman              # full 모드 (기본값)
/caveman lite         # 가벼운 압축
/caveman ultra        # 극단적 압축
/caveman wenyan       # 고전 중국어
stop caveman          # 일반 산문으로 복귀
```

## 출력 예시

질문: "React 컴포넌트가 왜 리렌더링돼?"

일반 산문:
> Your component re-renders because you create a new object reference each render. Wrapping it in `useMemo` will fix the issue.

케이브맨 (full):
> 렌더마다 새 객체 ref 생성. 인라인 객체 prop = 새 ref = 리렌더. `useMemo` 감싸.

케이브맨 (ultra):
> 인라인 obj prop → 새 ref → 리렌더. `useMemo`.

## 참고

- [`SKILL.md`](./SKILL.md) — 전체 LLM 지시 사항
- [Caveman README](../../README.md) — 저장소 개요, 설치, 벤치마크
