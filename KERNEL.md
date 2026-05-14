# opencode-kernel

> Pure tracking fork of [`anomalyco/opencode`](https://github.com/anomalyco/opencode) (MIT, ~158K stars).

## What this repo is

This is a near-pristine mirror of upstream `anomalyco/opencode`, kept under the `kidsinai` org for two reasons:

1. **Upstream tracking** — periodic `git fetch upstream && git merge upstream/dev` to stay current with bug fixes, model adapters, and tool-use improvements.
2. **Optional contribution origin** — if we develop a generally useful improvement, we can branch from this fork and open an upstream PR.

## What this repo is NOT

This repo does **not** contain Airbotix / Kids in AI product code. The product lives at:

- **[`kidsinai/kids-opencode`](https://github.com/kidsinai/kids-opencode)** (private) — the kid-facing product: web UI, virtual filesystem, course-pack runner, parent audit log, DeepRouter integration.

The product repo consumes opencode purely as a dependency via:

- `@opencode-ai/sdk` (npm) — server client
- `@opencode-ai/plugin` (npm) — plugin / hook registration

No code from this kernel repo is imported directly by the product.

## Branch policy

- Default branch: `dev` (matches upstream)
- We do not maintain feature branches here. Product feature work happens in `kidsinai/kids-opencode`.

## Sync workflow

```bash
git fetch upstream
git merge upstream/dev          # or: git rebase upstream/dev
git push origin dev
```

Cherry-pick individual upstream commits only when we need a fix before upstream cuts a release.

## Why a separate repo

See `kidsinai/kids-opencode` PRD / PLAN for the rationale behind the two-repo split (decision date 2026-05-14).
