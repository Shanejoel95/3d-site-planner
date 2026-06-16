# North Star — Deconstructing igloo.inc

https://www.igloo.inc/ · Awwwards Site of the Day + Developer Award (3D / Technology).
This is the bar the user wants to hit. Use it as the worked example of *what
award-tier looks like and why* — and as the template for how to deconstruct any
reference the client points at.

## Why it won (what to actually copy)

Award-tier isn't "more 3D." igloo scored **Animations/Transitions 9.60** and **WPO
8.00** — judges rewarded **motion quality plus the fact that heavy 3D still performed
well.** The formula, in priority order:

1. **One coherent metaphor, executed end-to-end.** "Igloo" → a procedural ice/crystal
   world; every project lives encased in a grown ice block. The concept drives every
   scene, not decoration bolted on. *This is the single most important thing — nail
   the metaphor before any tech.*
2. **UI and 3D in one WebGL context.** The entire UI is rendered in WebGL (text via
   SDF textures), so motion is unified and frame-perfect — no DOM/canvas seam.
3. **Procedural systems that scale.** A crystal-growth algorithm generates structure
   from a base shape, so new content doesn't need hand-modeling.
4. **Performance is invisible, not absent.** Custom compact geometry exporters; load
   textures and compile shaders both up-front and in the background to avoid
   shader-compile stutter; a custom VDB→browser volume exporter for the footer fluid,
   compressed "smaller than a typical website image."

**The honest tradeoff (flag this in every plan):** a fully-WebGL UI tanks
accessibility/SEO — igloo scored Accessibility 6.60, Semantics/SEO 6.40. For a client
who needs to rank or be ADA-compliant, you **must** keep real text in the DOM and ship
a crawlable fallback. Don't blindly copy the all-canvas approach.

## The stack (confirmed)

- **Three.js** (raw WebGL — *not* R3F, *not* WebGPU, *not* Unreal)
- **Svelte** for app structure; **GSAP** for animation/timeline orchestration
- **three-mesh-bvh** for fast raycasting; **Vite** build
- Heavy **proprietary in-house tooling** (a live in-browser editor)
- Content pipeline: **Houdini** + **Blender** (sim/model/texture)

> Takeaway for recommendations: the *stack* is replaceable (most studios would ship
> this on R3F + drei + Lenis + GSAP). The *discipline* — one metaphor, unified
> rendering, procedural scale, hidden load cost — is what's non-negotiable.

## Signature moments (the vocabulary to adapt)

- **Continuous scroll-driven camera journey** through one connected world (no hard
  page cuts).
- **Real-time intro animation** rendered in-engine (no pre-rendered video), flowing
  straight into the scene so there's no load wait and one consistent look.
- **Scene transitions:** chromatic aberration + "tech displacement" + frost/dissolve.
- **Particle navigation:** swirling points **coalesce into a different 3D shape per
  hovered link**; particles **shift color by velocity** and **glow** as they morph,
  synced to music/SFX.
- **Process discipline:** "wow moments" were **greyboxed/previs'd** (untextured
  real-time) to validate the journey *before* committing to expensive procedural work.

## How to deconstruct ANY reference (apply this to client-named sites)

When the client (or you) points at a site to emulate, research and answer:
1. **Concept** — what's the one metaphor/idea? Could you describe the site in a sentence?
2. **Signature moment** — the single thing people remember. What is it, mechanically?
3. **Stack & libraries** — engine (Three.js / R3F / WebGPU / Spline), scroll (Lenis /
   GSAP ScrollTrigger), shaders, post-processing. Search Awwwards case studies,
   Codrops, the threejs forum, the studio's writeup, "made of" / built-with tools.
4. **Motion system** — scroll choreography, camera moves, transitions, hover states.
5. **Performance & loading** — preloader, asset budgets, mobile behavior, fallbacks.
6. **The tradeoff it accepted** — what did it sacrifice (SEO? load? accessibility?),
   and is that acceptable for *this* client?

Feed the answers into the plan's **Motion & animation system** and **Recommended 3D
approach** sections, with the reference cited. See `animation-techniques.md` for the
library/technique vocabulary to express the answers in.

## Sources
- https://www.awwwards.com/sites/igloo-inc · https://www.awwwards.com/igloo-inc-case-study.html
- https://okaydev.co/u/vlucendo/portfolio/igloo-inc
- https://discourse.threejs.org/t/landing-site-igloo-inc/67249
- https://www.webgpu.com/showcase/igloo-inc-procedural-crystals/
