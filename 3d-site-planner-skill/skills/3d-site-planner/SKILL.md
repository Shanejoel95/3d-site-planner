---
name: 3d-site-planner
description: >-
  Research a prospective client (existing website, Google reviews, articles,
  videos, photos, social presence, brand assets), surface their highlights and
  drawbacks, then produce a complete 3D / WebGL website build plan: analysis,
  build brief (sitemap, 3D scene concepts, copy direction, asset list,
  interactions, performance budget, fallbacks), and a phased delivery roadmap —
  with a 3D stack recommended PER CLIENT (Three.js / React Three Fiber vs Spline
  vs hybrid vs 3D-lite). Use this skill whenever the user wants to plan, scope,
  audit, propose, or pitch a 3D / immersive / WebGL / interactive website for a
  client or business; whenever they paste a URL, business name, reviews, or notes
  about a client and ask what to build or how to approach it; or whenever they
  ask for a website proposal, discovery, intake, audit, or roadmap — even if they
  don't explicitly say "3D" or "plan".
---

# 3D Site Planner

Turn raw, messy client information into a confident, buildable plan for a 3D
website. The output is a single decision document the user can act on, share with
the client, or hand to a builder (including a later "build the site" skill).

The core idea: **never plan in a vacuum.** Two clients in the same industry need
very different sites depending on their reputation, existing assets, audience, and
budget. So always research first, then let the findings drive the recommendation —
especially the choice of 3D stack, which is the decision most people get wrong.

## Workflow at a glance

1. **Gather** — combine what the user gave you with what you can fetch yourself.
2. **Analyze** — build a clear picture: highlights to amplify, drawbacks to fix.
3. **Recommend a 3D approach** — pick the stack that fits *this* client.
4. **Write the build brief** — sitemap, scenes, copy, assets, interactions, perf.
5. **Lay out a phased roadmap** — what happens when, with deliverables and effort.
6. **Deliver** — assemble everything into the plan document and save it.

Do all six in one pass. Don't stop to ask permission between phases unless a
genuine blocker appears (e.g. the business can't be identified at all).

---

## Phase 1 — Gather the data

You will almost always get a *partial* picture from the user. Your job is to fill
the gaps yourself, then plan from the union of both.

**Use everything the user provided** — URLs, business name + location, pasted
reviews, screenshots, brand colors, notes, "they don't have a site," budget hints,
deadlines. Treat these as ground truth.

**Then fetch what's missing.** Read `references/research-checklist.md` for the full
source list and the exact signals to extract from each. In short:

- If there's a **website**, fetch it (home + key pages) and audit it firsthand —
  don't guess from the homepage alone.
- If there's **no website**, that's a finding, not a dead end — it usually means a
  bigger opportunity and a from-scratch brand/content effort. Note it explicitly.
- Search for **Google reviews / ratings**, **news or articles**, **YouTube or
  social video**, **photos** (do they have shootable/product imagery?), and
  **social profiles** (Instagram/LinkedIn/Facebook/TikTok).
- Pull **2–3 competitors** for visual and positioning benchmarking.

Use `web_search` to find sources and `web_fetch` to read the important ones in
full — snippets are not enough to audit a site. Run a separate search per data
type rather than one mega-query. If a source genuinely can't be found, say so in
the plan instead of inventing it. **Never fabricate reviews, quotes, or stats.**

Stop gathering when you can confidently describe: who they are, how they're
perceived, what assets exist, who they're selling to, and what's holding the
current presence back.

---

## Phase 2 — Analyze

Convert raw findings into a structured read. Score the client across the
dimensions in `references/analysis-rubric.md` (digital presence, brand assets,
reputation, content readiness, 3D-fit, etc.) and use those scores to derive two
honest lists:

- **Highlights** — real strengths and assets to *amplify* in the 3D build (e.g.
  strong reviews → social-proof scene; great product photography → 3D product
  showcase; distinctive brand → signature hero interaction).
- **Drawbacks / gaps** — what's *missing or working against them* and must be
  addressed (e.g. no photography → budget for a shoot or AI/3D assets; thin copy →
  messaging workshop; slow legacy site → performance is a primary goal).

Be specific and evidence-based. "Reviews praise their fast turnaround (4.8★, 200+
reviews)" beats "good reputation." Tie each drawback to something the plan will
actually do about it — an unaddressed drawback is a planning miss.

Also capture: target audience, primary conversion goal (call, booking, purchase,
lead form), competitive positioning, and any hard technical constraints (CMS lock,
e-commerce platform, multilingual, accessibility/regulatory needs).

---

## Phase 3 — Recommend the 3D approach

This is the highest-leverage decision in the plan. **Don't default to heavy
Three.js for everyone.** Read `references/3d-stack-selection.md` and pick the
approach that matches the client's budget, brand, content, performance needs, and
who will maintain the site:

- **Three.js / React Three Fiber** — custom WebGL; maximum control and
  distinctiveness; highest cost/effort.
- **Spline (or similar no-code 3D)** — fast, designer-friendly, easy handoff; less
  custom logic; watch bundle size.
- **Hybrid** — Spline/exported assets dropped into a React/Three scene; pragmatic
  middle ground.
- **3D-lite** — scroll-driven, parallax, CSS 3D, subtle WebGL accents; best when
  budget/performance/SEO dominate and full 3D would be overkill.

State the recommendation, *why it fits this client specifically*, the realistic
tradeoffs, and a fallback approach if budget or timeline tightens. Always pair the
3D choice with a non-3D fallback experience for low-power devices and crawlers.

---

## Phase 4 — Write the build brief

The actionable core. Specify, concretely:

- **Sitemap** — pages/sections and their purpose.
- **3D scene concepts** — per page or per key section: what's in the scene, the
  interaction, what it communicates, and how it serves the conversion goal. Ground
  these in the highlights from Phase 2.
- **Signature hero concept** — the one memorable moment that defines the site.
- **Copy direction** — voice, key messages, headline angles (derived from real
  reviews/positioning, not generic filler). Draft hero/section headlines.
- **Asset list** — 3D models, textures, photography, video, icons, fonts: what
  exists, what to source, what to create (and how — shoot, model, AI-generate).
- **Interactions & motion** — scroll behavior, hover/click states, transitions.
- **Performance budget** — target load, asset weight ceilings, lazy-loading,
  mobile strategy.
- **Accessibility & fallbacks** — reduced-motion, keyboard nav, crawlable content.
- **SEO & analytics** — metadata, structured data, what to measure.

---

## Phase 5 — Phased roadmap

Lay out delivery in clear phases — typically Discovery → Design/Prototype → 3D
Asset Production → Build → QA & Performance → Launch → Post-launch. For each:
deliverables, a rough effort/duration estimate, dependencies, and key risks. Be
honest about where 3D adds time (asset production, optimization, cross-device QA).
Flag the biggest risk to the timeline up front.

---

## Output — ALWAYS assemble the full plan

Produce **one** structured plan document following `references/plan-template.md`
exactly (sections in order). Save it as a markdown file in
`/mnt/user-data/outputs/` named after the client (e.g.
`acme-dental-3d-site-plan.md`) and present it. After delivering, offer to also
export it as PDF or a Word doc, or to draft a client-facing proposal version.

Keep the writing concise and practical — skip filler, prefer tight bullets and
short paragraphs, and make every recommendation traceable to a finding.

## Principles

- Research first; let evidence drive recommendations.
- Right-size the 3D — distinctiveness and performance must coexist.
- Every drawback gets a corresponding action in the plan.
- Never invent reviews, metrics, quotes, or sources.
- The plan should be specific enough that someone could start building from it.
