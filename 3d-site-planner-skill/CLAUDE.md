# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this repo is

A single Claude skill, `3d-site-planner`, that researches a client and produces a
complete 3D website plan (analysis + build brief + phased roadmap). It is packaged
as a Claude Code plugin (`.claude-plugin/`) and as a Claude.ai skill upload
(`dist/3d-site-planner.skill`).

## Layout

- `.claude/skills/3d-site-planner/SKILL.md` — the skill: 6-phase workflow.
- `.claude/skills/3d-site-planner/references/` — checklists, the stack-selection
  matrix, the scoring rubric, and the output template. Read on demand.
- `examples/` — worked examples of the skill's output.
- `dist/` — the `.skill` package for Claude.ai.

## When editing the skill

- Keep `SKILL.md` under ~500 lines; push detail into `references/`.
- Re-package the `.skill` after changes if you want `dist/` to stay current.
- Don't introduce dependencies — this skill is instruction-driven and uses the
  host's own web search / fetch tools at runtime.
