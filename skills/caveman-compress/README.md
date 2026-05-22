<p align="center">
  <img src="https://em-content.zobj.net/source/apple/391/rock_1faa8.png" width="80" />
</p>

<h1 align="center">caveman-compress</h1>

<p align="center">
  <strong>메모리 파일 압축. 매 세션마다 토큰 절감.</strong>
</p>

---

프로젝트 메모리 파일(`CLAUDE.md`, 할 일 목록, 설정)을 케이브맨 형식으로 압축하는 Claude Code 스킬 — 매 세션마다 자동으로 더 적은 토큰 로드.

Claude는 매 세션 시작 시 `CLAUDE.md`를 읽음. 파일 크면 비용 큼. 케이브맨이 파일 작게 만듦. 비용 영원히 낮아짐.

## 기능

```
/caveman-compress CLAUDE.md
```

```
CLAUDE.md          ← 압축본 (Claude가 읽음 — 매 세션 토큰 절감)
CLAUDE.original.md ← 사람이 읽는 백업 (이걸 편집)
```

원본 안 잃음. `.original.md` 읽고 편집 가능. 편집 후 스킬 다시 실행해 재압축.

## 벤치마크

실제 프로젝트 파일 실측값:

| 파일 | 원본 | 압축 | 절감 |
|------|-----:|-----:|-----:|
| `claude-md-preferences.md` | 706 | 285 | **59.6%** |
| `project-notes.md` | 1145 | 535 | **53.3%** |
| `claude-md-project.md` | 1122 | 636 | **43.3%** |
| `todo-list.md` | 627 | 388 | **38.1%** |
| `mixed-with-code.md` | 888 | 560 | **36.9%** |
| **평균** | **898** | **481** | **46%** |

검증 전체 통과 ✅ — 헤딩, 코드 블록, URL, 파일 경로 정확 보존.

## 전후 비교

<table>
<tr>
<td width="50%">

### 📄 원본 (706 토큰)

> "I strongly prefer TypeScript with strict mode enabled for all new code. Please don't use `any` type unless there's genuinely no way around it, and if you do, leave a comment explaining the reasoning. I find that taking the time to properly type things catches a lot of bugs before they ever make it to runtime."

</td>
<td width="50%">

### <img src="../../docs/assets/dancing-rock.svg" width="20" height="20" alt="rock"/> 케이브맨 (285 토큰)

> "Prefer TypeScript strict mode always. No `any` unless unavoidable — comment why if used. Proper types catch bugs early."

</td>
</tr>
</table>

**같은 지시 사항. 60% 적은 토큰. 매. 번. 세션.**

## 보안

`caveman-compress`는 정적 분석이 감지한 subprocess 및 파일 I/O 패턴으로 인해 Snyk High Risk 플래그가 붙음. 이는 오탐 — 스킬이 하는 것과 하지 않는 것에 대한 전체 설명은 [SECURITY.md](./SECURITY.md) 참고.

## 설치

compress는 `caveman` 플러그인에 내장. `caveman` 한 번 설치 후 `/caveman-compress` 사용.

로컬 파일이 필요하면 compress 스킬 위치:

```bash
caveman-compress/
```

**요구 사항:** Python 3.10+

## 사용법

```
/caveman-compress <파일경로>
```

예시:
```
/caveman-compress CLAUDE.md
/caveman-compress docs/preferences.md
/caveman-compress todos.md
```

### 압축 가능한 파일

| 유형 | 압축? |
|------|-------|
| `.md`, `.txt`, `.rst`, `.typ`, `.typst`, `.tex` | ✅ 가능 |
| 확장자 없는 자연어 파일 | ✅ 가능 |
| `.py`, `.js`, `.ts`, `.json`, `.yaml` | ❌ 제외 (코드/설정) |
| `*.original.md` | ❌ 제외 (백업 파일) |

## 동작 방식

```
/caveman-compress CLAUDE.md
        ↓
파일 유형 감지        (토큰 없음)
        ↓
Claude 압축          (토큰 — 한 번 호출)
        ↓
출력 검증            (토큰 없음)
  검사: 헤딩, 코드 블록, URL, 파일 경로, 불릿
        ↓
오류 시: Claude가 선택적 수정만   (토큰 — 타겟 수정)
  재압축 안 함 — 깨진 부분만 패치
        ↓
최대 2회 재시도
        ↓
압축본 → CLAUDE.md 기록
원본   → CLAUDE.original.md 기록
```

토큰 사용: 초기 압축 + 검증 실패 시 타겟 수정만. 나머지는 로컬 Python.

## 보존되는 것

케이브맨은 자연어를 압축. 다음은 절대 건드리지 않음:

- 코드 블록 (` ``` ` 펜스 또는 들여쓰기)
- 인라인 코드 (`` `백틱 내용` ``)
- URL과 링크
- 파일 경로 (`/src/components/...`)
- 명령어 (`npm install`, `git commit`)
- 기술 용어, 라이브러리 이름, API 이름
- 헤딩 (정확한 텍스트 보존)
- 표 (구조 보존, 셀 텍스트 압축)
- 날짜, 버전 번호, 숫자 값

## 왜 중요한가

`CLAUDE.md`는 **매 세션 시작마다** 로드됨. 1000 토큰짜리 프로젝트 메모리 파일은 프로젝트 열 때마다 토큰 비용 발생. 100회 세션이면 이미 작성한 컨텍스트를 위한 오버헤드만 100,000 토큰.

케이브맨이 평균 ~46% 절감. 같은 지시 사항. 같은 정확도. 낭비 감소.

```
┌────────────────────────────────────────────┐
│  파일당 토큰 절감     █████       46% │
│  혜택 받는 세션       ██████████ 100% │
│  정보 보존            ██████████ 100% │
│  설정 시간            █            1x │
└────────────────────────────────────────────┘
```

## Caveman의 일부

이 스킬은 [caveman](https://github.com/alpakalee/caveman) 툴킷의 일부 — Claude가 정확도 손실 없이 더 적은 토큰 사용하게 만들기.

- **caveman** — Claude가 케이브맨처럼 *말하게* 함 (응답 토큰 ~65% 절감)
- **caveman-compress** — Claude가 *덜 읽게* 함 (컨텍스트 토큰 ~46% 절감)
