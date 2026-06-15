# 3D Site Planner

<p align="center">
  <img src="https://img.shields.io/badge/Claude-Skill-D97757?style=for-the-badge" alt="Claude Skill">
  <img src="https://img.shields.io/badge/version-1.0.0-blue?style=for-the-badge" alt="Version 1.0.0">
  <a href="LICENSE"><img src="https://img.shields.io/github/license/Shanejoel95/3d-site-planner-skill?style=for-the-badge&color=green" alt="License"></a>
  <a href="https://github.com/Shanejoel95/3d-site-planner-skill/stargazers"><img src="https://img.shields.io/github/stars/Shanejoel95/3d-site-planner-skill?style=for-the-badge&logo=github" alt="Stars"></a>
</p>

**A Claude skill that turns messy client information into a buildable plan for a 3D website.**

Most "plan my website" prompts answer from thin air. This skill does the opposite:
it researches the client first — pulling whatever exists (a live site, Google
reviews, articles, video, photos, social) and combining it with whatever you supply —
then produces one decision document you can act on, hand to a client, or feed
straight to a build skill.

The output is a complete plan: an evidence-based analysis (highlights to amplify,
drawbacks to fix), a **3D stack recommendation chosen per client** (Three.js / React
Three Fiber vs Spline vs hybrid vs 3D-lite), a build brief, and a phased roadmap.

---

## Why it exists

Two businesses in the same industry need very different sites depending on their
reputation, existing assets, audience, and budget. And the single most-botched
decision in 3D web work is reaching for heavy custom WebGL when a lighter approach
would ship faster, perform better, and stay maintainable. This skill makes both
calls on evidence instead of vibes.

## What it does

1. **Gather** — uses what you give it *and* fetches the rest (reviews, articles,
   video, photos, social, 2–3 competitors). "No website" is treated as an
   opportunity, not a dead end.
2. **Analyze** — scores the client on 10 dimensions, then derives an honest
   **Highlights** list (assets to amplify) and **Drawbacks/gaps** list (each paired
   with the fix).
3. **Recommend a 3D approach** — picks the stack that fits *this* client, with
   tradeoffs and a fallback.
4. **Build brief** — sitemap, per-page 3D scene concepts, signature hero, copy
   direction, asset list, interactions, performance budget, accessibility, SEO.
5. **Roadmap** — phased delivery with deliverables, effort, and risks.
6. **Deliver** — assembles everything into one structured plan document.

It never fabricates reviews, quotes, or stats, and it always pairs the 3D choice
with a crawlable non-3D fallback for low-power devices and search engines — the
thing most 3D plans skip.

## Install

### Claude Code (plugin)

```
/plugin marketplace add Shanejoel95/3d-site-planner-skill
/plugin install 3d-site-planner@3d-site-planner-skill
```

The skill auto-activates whenever you ask to plan, scope, or pitch a 3D website.

### Claude.ai / Claude apps (skill upload)

Download [`dist/3d-site-planner.skill`](dist/3d-site-planner.skill) and upload it in
**Settings → Capabilities → Skills**.

### Manual (any assistant that reads `.claude/skills/`)

Copy `.claude/skills/3d-site-planner/` into your project's `.claude/skills/` folder.

## Usage

Just describe the client. Examples:

```
Plan a 3D website for Serenity Spa in Colombo.

Here's a client: https://example-dental.com — what 3D site should we build?

Plan an immersive site for a boutique furniture brand. They have great product
photos but no website yet.
```

The skill researches, analyzes, and writes the plan. See a full worked example in
[`examples/uupm-3d-site-script.md`](examples/uupm-3d-site-script.md) — a creative,
implementable 3D scroll narrative produced from a real project's data.

## What's in the box

```
.claude/skills/3d-site-planner/
├── SKILL.md                        # workflow + how the phases run
└── references/
    ├── research-checklist.md       # every data source + signals to extract
    ├── 3d-stack-selection.md       # Three.js / Spline / hybrid / 3D-lite matrix
    ├── analysis-rubric.md          # 10-dimension scorecard → highlights/drawbacks
    └── plan-template.md            # exact output structure
examples/
└── uupm-3d-site-script.md          # worked example
dist/
└── 3d-site-planner.skill           # upload package for Claude.ai
```

The reference files load only when needed, so the skill stays lightweight until it
is actually working.

## Pairs well with

A UI/UX design-intelligence skill (e.g.
[ui-ux-pro-max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)) for the
2D token system — let that own typography, components, spacing, and the
pre-delivery checklist, and let this skill own the research, the 3D direction, and
the roadmap.

## Output structure

Every plan follows a fixed template: executive summary → client snapshot → research
findings → analysis (scorecard + highlights + drawbacks) → recommended 3D approach →
build brief → phased roadmap → open questions.

## Contributing

Issues and PRs welcome — especially additions to the research checklist, the stack
selection matrix, and new worked examples.

## License

MIT — see [LICENSE](LICENSE).
