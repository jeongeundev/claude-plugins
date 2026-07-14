# tdd-guard

Claude Code 플러그인. 테스트 우선(TDD) 순서를 **훅으로 강제**한다.

`PreToolUse[Edit|Write]` 훅이 소스 파일 작성/수정을 가로채, 대응하는 테스트 파일이 먼저 존재하지 않으면 도구 실행을 차단(`deny`)한다. 즉 구현 코드를 쓰기 전에 테스트부터 작성하게 만든다(red → green).

## 설치

```
/plugin marketplace add jeongeundev/claude-plugins
/plugin install tdd-guard@jeongeundev-plugins
```

설치한 세션에서만 가드가 활성화된다. 설치하지 않은 사람에게는 영향이 없다.

## 동작 규칙

- **차단 대상:** `.ts` / `.tsx` / `.js` / `.jsx` 소스 파일 중 대응 테스트가 없는 경우.
- **테스트 탐색 위치:** ① 같은 폴더의 `<name>.test.*` / `<name>.spec.*` → ② `__tests__/` (같은 폴더 또는 상위 폴더) → ③ git 루트의 `src/__tests__/`.
- **예외(항상 허용):**
  - 테스트/스펙 파일 자체 (`*test*`, `*spec*`, `*__tests__*`)
  - 설정·문서·스타일 (`.json` / `.css` / `.scss` / `.md` / `.yml` / `.yaml` / `.env*` / `.config.*` / `tailwind` / `postcss` / `next.config` / `tsconfig`)
  - 타입 (`types/` 폴더, `types.ts`, `types.d.ts`)
  - Next.js 프레임워크 파일 (`layout` / `page` / `loading` / `error` / `not-found`, `globals.css`)

차단 시 다음과 같은 메시지가 표시된다:

```
TDD GUARD: '<name>'에 대한 테스트 파일이 존재하지 않습니다.
구현 코드를 작성하기 전에 테스트를 먼저 작성하세요. (테스트 파일 예: <name>.test.ts)
```

## 사전 요구사항

- `bash`, `jq` (훅 스크립트가 stdin JSON을 파싱하는 데 사용).

## 구조

```
tdd-guard/
├── .claude-plugin/plugin.json
├── hooks/hooks.json          # PreToolUse[Edit|Write] → scripts/tdd-guard.sh
└── scripts/tdd-guard.sh
```

훅 커맨드는 `${CLAUDE_PLUGIN_ROOT}` 기준 경로로 스크립트를 참조하므로 설치 위치와 무관하게 동작한다.
