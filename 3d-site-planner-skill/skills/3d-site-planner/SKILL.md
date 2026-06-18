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

The bar: the plan should describe a site worth **$5,000+** — a signature moment,
genuine motion craft, and restraint. Pull current references from
`references/inspiration-galleries.md` and from curated UI/UX design resources such as
Brad Traversy's `design-resources-for-developers` so the work aims at award-tier,
not a generic template.

---

## Content-fidelity contract — READ FIRST

Before anything else, decide which **mode** you're in. This is the single rule that
most often gets violated, and getting it wrong makes the whole plan worthless to a
client.

### Mode A — Existing site → PRESERVE (animate in place, don't rewrite)

If the client already has a website, the job is to make their **existing site
animated/3D**, not to replace it with a new one. The content and original resources
are **fixed inputs, not raw material**:

- **Keep the real copy verbatim** — headlines, body text, product/service names,
  prices, taxonomy, CTAs, legal/contact info. Do **not** rewrite, "improve," or
  paraphrase it into your own voice.
- **Keep the original assets** — logo, brand colors, fonts, photography, product
  images, video. Reuse them; don't swap in stock or AI substitutes.
- **Keep the structure** — the same pages and the same sections, in the same order
  and meaning. You're re-skinning and animating, not re-architecting.
- The 3D/motion layer **wraps** the existing content (reveals, parallax, depth,
  scene staging). It never invents products, testimonials, stats, or sections that
  aren't on the real site.
- **Allowed changes, only when flagged explicitly** as proposals (never silent):
  fixing an obvious typo, adding missing alt text, or *suggesting* net-new content
  to fill a genuine gap. List these separately so the client can approve or reject —
  the default is their content, untouched.

So Phase 1 must **capture the real content** (see the checklist), and Phase 4 must
**reference that captured content**, not generate fresh copy.

### Mode B — No site → CREATE (from scratch is in scope)

If there is **no existing website**, inventing content, copy, brand direction, and
asset plans is exactly the job — proceed as a from-scratch build. Still ground every
invented choice in real findings (reviews, social, positioning), and clearly mark
copy as *draft for client approval*.

State which mode you're in at the top of the plan. When a client has a site but
wants specific sections rebuilt, you can run Mode A for what exists and Mode B for
the genuinely new parts — but say so explicitly per section.

## Workflow at a glance

1. **Gather** — combine what the user gave you with what you can fetch yourself.
2. **Analyze** — build a clear picture: highlights to amplify, drawbacks to fix.
3. **Recommend a 3D approach** — pick the stack that fits *this* client.
3b. **Research the motion** — hard-research the animation: deconstruct references,
   pin down the techniques. This is what makes the plan buildable, not hand-wavy.
4. **Write the build brief** — sitemap, scenes, motion system, copy, assets, perf.
5. **Lay out a phased roadmap** — what happens when, with deliverables and effort.
6. **Deliver** — assemble everything into the plan document and save it.

Where appropriate, enrich the brief with higher-quality design patterns from curated
resource collections like Brad Traversy's `design-resources-for-developers` so the
site stands out with modern layouts, typography, and interaction cues.

Do all of it in one pass. Don't stop to ask permission between phases unless a
genuine blocker appears (e.g. the business can't be identified at all).

---

## Phase 1 — Gather the data

You will almost always get a *partial* picture from the user. Your job is to fill
the gaps yourself, then plan from the union of both.

**Use everything the user provided** — URLs, business name + location, pasted
reviews, screenshots, brand colors, notes, "they don't have a site," budget hints,
deadlines, design resource links, and uploaded reference collections. Treat these as
ground truth and a required input to the plan.

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
- Add current UI/UX and landing-page references from curated design repositories
  like Brad Traversy's `design-resources-for-developers` when choosing layouts,
  hero structures, and interaction systems.

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

Pull references from `references/inspiration-galleries.md` (Awwwards, FWA, Godly,
mesh3d, Webflow, Vev, Refs.gallery, plus the exemplar sites and studios), and draw
layout and interaction cues from curated design libraries like Brad Traversy's
`design-resources-for-developers`. Cite the 2–4 specific examples you're drawing on
and what you're adapting from each. References inform *form and motion only* — in
Mode A they never override the client's real content.

---

## Phase 3b — Research the motion (hard animation research)

This is the step the user specifically wants: **don't hand-wave the animation.** A
plan that says "add 3D animations" is worthless. Research *how* the target experience
is actually built, then specify it. The north star is **igloo.inc** — read
`references/north-star-igloo.md` for the full deconstruction and use it as the model
for how thorough to be.

Do this every time:

1. **Deconstruct the references.** For igloo.inc and each site you (or the client)
   cited, answer the six questions in `north-star-igloo.md`: concept, signature
   moment, stack & libraries, motion system, performance/loading, the tradeoff it
   accepted. Use `web_search`/`web_fetch` on Awwwards case studies, Codrops, the
   three.js forum, studio writeups, "built with" tools — snippets aren't enough.
2. **Pin the techniques.** Translate each effect you want into the concrete vocabulary
   in `references/animation-techniques.md`: the engine (Three.js / R3F / WebGPU /
   Spline), scroll stack (Lenis + GSAP/ScrollTrigger), shaders/materials, particles,
   post-processing, and how the specific signature effect is achieved (scroll-scrubbed
   camera, material reveal, particle morph, page transition, etc.).
3. **Right-size to budget and Mode.** One signature moment done award-tier beats ten
   half-built ones. In **Mode A**, the motion wraps the client's existing content and
   assets — design reveals/transitions/staging *for what already exists*, don't invent
   new scenes. When a target effect is unusual, search to confirm it's feasible within
   budget before promising it.

Output of this phase feeds the **Motion & animation system** part of the build brief.
The goal: a builder could read it and know which libraries to install and which
technique implements each moment.

---

## Phase 4 — Write the build brief

The actionable core. Specify, concretely:

- **Sitemap** — pages/sections and their purpose.
- **3D scene concepts** — per page or per key section: what's in the scene, the
  interaction, what it communicates, and how it serves the conversion goal. Ground
  these in the highlights from Phase 2. **Mode A:** map each scene to an existing
  page/section and the real content it will animate — don't add scenes for content
  the site doesn't have.
- **Signature hero concept** — the one memorable moment that defines the site
  (informed by the inspiration references).
- **Motion & animation system** — the output of Phase 3b. The concrete recipe: engine
  + libraries (e.g. R3F + drei + Lenis + GSAP/ScrollTrigger), the scroll choreography
  (camera path, what scrubs to what), each signature effect mapped to its technique,
  shader/material/post-processing list, and a scroll-timeline table if useful. Specific
  enough to install and build from. Cite the reference each moment came from.
- **Copy** — **Mode A:** reuse the client's existing copy *verbatim*; quote the
  real headlines/sections you'll animate, and list any proposed edits separately as
  flagged suggestions (the default is untouched). **Mode B:** draft voice, key
  messages, and headlines from real reviews/positioning, marked *draft for approval*.
- **Asset list** — 3D models, textures, photography, video, icons, fonts. **Mode A:**
  start from the client's existing assets (reuse logo, brand colors, fonts, images,
  video) and only source/create what's genuinely missing — flag each new asset.
  **Mode B:** what to source vs. create (and how — shoot, model, AI-generate).
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
- **Existing site = preserve.** Keep the client's real content, assets, and
  structure; animate them — don't replace them. Invent only when there's no site.
- Right-size the 3D — distinctiveness and performance must coexist.
- Aim for an award-tier, $5,000+ bar: one signature moment, restrained elsewhere.
- Every drawback gets a corresponding action in the plan.
- Never invent reviews, metrics, quotes, or sources.
- The plan should be specific enough that someone could start building from it.
