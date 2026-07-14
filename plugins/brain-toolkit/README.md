# brain-toolkit

Claude Code 플러그인. 두 갈래의 스킬을 번들한다.

1. **레포 감사** — `ai-readiness-cartography`: 임의 레포를 AI-Ready v2 루브릭(100점·7카테고리)으로 채점하고 단일 HTML 대시보드 + ROI 액션 리스트를 만든다.
2. **세컨드 브레인 wiki** — `wiki-ingest` / `wiki-query` / `wiki-lint`: Karpathy식 LLM wiki(vault)를 누적·질의·점검한다.

## 설치

```
/plugin marketplace add jeongeundev/claude-plugins
/plugin install brain-toolkit@jeongeundev-plugins
```

## 스킬

설치하면 플러그인 이름으로 네임스페이스된 슬래시 커맨드로 노출된다.

| 커맨드 | 하는 일 |
|---|---|
| `/brain-toolkit:ai-readiness-cartography` | 레포를 AI-Ready 루브릭으로 채점 → JSON + HTML 대시보드 + ROI 액션 |
| `/brain-toolkit:wiki-ingest` | `raw/` 소스를 읽어 wiki로 병합 통합(교차링크·모순 보존) |
| `/brain-toolkit:wiki-query` | wiki를 근거로 질문에 답(인용) + 가치 있는 답을 새 페이지로 환류 |
| `/brain-toolkit:wiki-lint` | wiki 건강검진 — 모순·고아·끊긴 링크·index·낡은 정보 점검 |

키워드/자연어로도 자동 트리거된다(예: "이 레포 agent-friendly한지 점수 매겨줘", "이거 위키에 넣어줘").

## 사전 요구사항

- **ai-readiness-cartography**: `python3` (3.10+). 스크립트는 stdlib only, 외부 의존성 없음. 결과 HTML은 인라인 SVG/CSS 단일 파일.
- **wiki-ingest / query / lint**: 실행 시점의 작업 디렉터리가 **Karpathy식 wiki vault**여야 한다 — 루트에 `WIKI_SCHEMA.md`(규칙의 단일 출처)와 `wiki/`·`raw/` 구조가 있어야 정상 동작한다. 세 스킬 모두 시작 시 `WIKI_SCHEMA.md`를 먼저 읽는다. 일반 코드 레포에서는 의미가 없다.

## 구조

```
brain-toolkit/
├── .claude-plugin/plugin.json
└── skills/
    ├── ai-readiness-cartography/   # SKILL.md + scripts/score.py + assets/ + references/
    ├── wiki-ingest/SKILL.md
    ├── wiki-query/SKILL.md
    └── wiki-lint/SKILL.md
```

번들된 스크립트는 `${CLAUDE_PLUGIN_ROOT}` 기준 경로로 참조하므로 설치 위치와 무관하게 동작한다.
