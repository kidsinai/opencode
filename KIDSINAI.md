# Kids in AI — opencode Fork Notes

> This file is **NOT from upstream** (`anomalyco/opencode` / formerly `sst/opencode`, MIT). It captures Kids OpenCode-specific intent and customisation plan, separately from upstream's `CLAUDE.md` (which we keep clean for rebase).

## What this fork is

The production repository for **Kids OpenCode** — Airbotix Kids in AI's flagship V0 product. An agentic AI coding tool for kids 12+, derived from `opencode` (158K-star open-source coding agent, MIT licensed, TypeScript stack).

Why fork instead of build:
- Saves 6–12 months of agent-runtime engineering
- Already model-agnostic (clean adapter pattern → swap to DeepRouter trivially)
- Tool use, plan/approve UX, diff/apply flow all implemented and battle-tested

## License inheritance

**MIT** (matches upstream). Our fork is intentionally public; the kid-facing UI layer + sandbox hardening will be the differentiator, not the agent core.

## What we customise (planned, not yet implemented)

**Minimise upstream changes** for sustainable rebase. Airbotix-specific code goes in dedicated locations:

| Where | What |
|---|---|
| Replace TUI → web UI | New React SPA (`packages/kids-web/` or similar) that talks to upstream agent core |
| Tool whitelist | Remove `Bash` from V0 (no command execution); keep `Read` / `Write` / `Edit` / `Glob` / `Grep` / `WebFetch` |
| Filesystem boundary | Virtual FS (Supabase Storage / Postgres BYTEA), not real OS files; path guard at tool entry |
| iframe preview | `<iframe sandbox="allow-scripts">` for kid's HTML/CSS/JS in their browser |
| Model adapter | Point at DeepRouter `/v1` (OpenAI-compatible) — single env var change |
| Audit log | Every tool call → POST to platform-backend audit endpoint |
| Workshop mode | Class context: Course Pack Mission, workshop credit pool (no family Stars) |
| Kid-safe system prompt | Wrap upstream prompt with our additional constraints |

## V0 scope (NARROW)

- **Languages**: HTML / CSS / JS **only**. No Python / Node / Bash / shell. No server-side code execution.
- **Hosting**: Hosted only. V1+ adds Tauri/Electron desktop.
- **Audience**: Kids 12+ (flagship Airbotix narrative).
- **First Course Pack**: "我的第一个 AI 项目 — 个人作品集网站" (3 Missions, ~30-50 Stars budget).

## V1+ expansion (post-PMF)

- Pyodide (Python in browser) — natural first expansion before any server-side container
- Server-side sandbox (gVisor / Firecracker) — only when course packs really need it
- Local desktop mode (Tauri preferred over Electron)
- Robotics bridge (WebUSB → Airbotix mBots)

## Spec source

| Doc | Location |
|---|---|
| Master plan | `~/Documents/sites/kidsinai/planning/PROJECT.md` |
| Full technical spec | `~/Documents/sites/airbotix/docs/product/prd/kids-opencode-spec.md` |
| Parent platform PRD | `~/Documents/sites/airbotix/docs/product/prd/kids-ai-platform-prd.md` |
| Compliance constraints | `~/Documents/sites/airbotix/docs/product/compliance/minors-compliance.md` |

## Upstream sync

```bash
git remote -v   # origin = our fork, upstream = anomalyco/opencode
git fetch upstream
git cherry-pick <commit>
```

## Sibling repos

- `kidsinai/creative-web` (frontend for 6-11 lower-age product line)
- `kidsinai/platform-backend` (shared backend, Family Account / Stars / Course Pack)
- `deeprouter-ai/deeprouter` (LLM gateway we depend on)
