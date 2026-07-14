# jeongeundev-plugins

Claude Code 플러그인 마켓플레이스. 팀에서 `/plugin`으로 설치해 공용 스킬을 공유한다.

## 설치

```
/plugin marketplace add jeongeundev/claude-plugins
/plugin install brain-toolkit@jeongeundev-plugins
```

설치 후 새 세션에서 스킬이 슬래시 커맨드로 노출된다(플러그인 이름으로 네임스페이스됨):

- `/brain-toolkit:ai-readiness-cartography`
- `/brain-toolkit:wiki-ingest`
- `/brain-toolkit:wiki-query`
- `/brain-toolkit:wiki-lint`

업데이트를 받으려면:

```
/plugin marketplace update jeongeundev-plugins
```

## 수록 플러그인

| 플러그인 | 내용 |
|---|---|
| [brain-toolkit](plugins/brain-toolkit) | AI-readiness cartography(레포 agent-적합도 감사 + HTML 대시보드) + 세컨드 브레인 wiki 툴킷(ingest·query·lint) |
