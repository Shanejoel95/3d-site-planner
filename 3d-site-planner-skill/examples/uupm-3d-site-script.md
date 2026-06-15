# UI UX Pro Max — 3D Site Script
### Working title: **"NOISE → SYSTEM"**

> The site *is* the product. You don't read about a reasoning engine that turns a
> messy idea into a finished design system — you fall into one, and watch it happen
> to you. Every scroll tick is one stage of the real pipeline
> (request → multi-domain search → reasoning → crystallized design system).

This is a scene-by-scene build script for a scroll-driven WebGL site. Each act has:
**the story**, **what you see**, **camera & motion**, **interaction**,
**implementation**, and **the uupm style it embodies** (using the skill's own
67-style taxonomy, so the site practices what it preaches).

---

## 0. The big idea & why it fits the data

The README's central diagram is a 4-stage pipeline: *request → 5 parallel searches
→ reasoning engine → complete design system*. That pipeline is the spine of the
site. The hero promise — "design intelligence" — is shown, not stated: the user
becomes the raw request and is reasoned into order.

Three numbers from the repo become the recurring 3D vocabulary:
- **161** rule-nodes (the lattice you fly through)
- **67** style-panes (the gallery near the end)
- **5** search beams (the moment intelligence "fans out")

And one anti-pattern from the repo becomes a design constraint: the skill flags
**"AI purple/pink gradients"** as a thing to avoid. So this site refuses the default
AI look. That refusal *is* the brand statement.

---

## Design language

**Palette (obsidian + bone + one electric accent — swap the accent via a single token):**
- `--void` `#0A0A0D` — deep obsidian base, the "unrendered" space
- `--graphite` `#16161C` — panels, fog, the lattice
- `--bone` `#EDE9E0` — warm off-white, all typography (paper, not pure white)
- `--signal` `#3D5AFE` — electric ultramarine, the accent of *order/intelligence*
- `--ember` `#FF6B3D` — warm amber, reserved ONLY for the ignition moment (Act 3)

Discipline: 90% obsidian/bone, signal used sparingly, ember used *once*. Bloom +
chromatic aberration carry the "alive" feeling instead of gradients.

**Type:** a sharp grotesk for kinetic display (e.g. *Space Grotesk* / *General Sans*)
+ a mono for the "machine readout" labels (e.g. *Geist Mono* / *JetBrains Mono*).
The contrast — humane display vs. machine mono — visually narrates "human intent
meets reasoning engine."

**Recurring motif — THE TOKEN:** one small luminous cube-octahedron (a "design
token"). It's the user's avatar. It enters as raw/jittering, and by the end it's
faceted, calm, and crowned with a tiny palette. The whole site is the token's
transformation from noise to system.

---

## Tech stack (recommended)

- **React Three Fiber** + **@react-three/drei** (`ScrollControls`, `useScroll`,
  `Instances`, `Environment`, `MeshTransmissionMaterial`, `Text`, `Float`).
- **@react-three/postprocessing** — `Bloom`, `ChromaticAberration`, `Vignette`,
  `Noise` (low), `DepthOfField`.
- **Lenis** for buttered scroll; drive timeline off `useScroll().offset`.
- **GSAP** (or `maath`/`damp`) for camera-path easing and per-act tweens.
- Custom **GLSL** for two signature effects: the search-beam scan and the
  crystallization snap.
- **Instanced meshes** for the 161-node lattice and the 67-pane gallery (one draw
  call each — non-negotiable for perf).
- Assets compressed with **Draco** (geometry) + **KTX2/Basis** (textures).

> Hybrid alternative if timeline is tight: author the hero token + lattice in
> **Spline**, export glb, and drop into R3F for the scroll logic. Drop to **3D-lite**
> (scroll-pinned canvas with 2D token + CSS chromatic split) only as the budget floor.

---

# THE SCRIPT

## ACT 1 — ARRIVAL (raw intent)
**Embodies:** *Kinetic Typography* + *Exaggerated Minimalism*

**The story.** You are an idea before it has form.

**What you see.** Pure `--void`. A single cursor blinks. A line of mono text types
itself — `> build me a landing page for a beauty spa` — the literal example from the
README. As the last character lands, the words **shatter into particles** and
collapse inward into one jittering, glitching **Token** floating dead-center, wrapped
in faint chromatic-aberration fringing (it's "unresolved"). Behind it, the wordmark
**UI UX PRO MAX** sits in huge bone grotesk, half-dissolved into the dark.

**Camera & motion.** Locked, shallow. The token trembles with Perlin noise; RGB
channels split a few px on the type. Everything feels *unstable on purpose*.

**Interaction.** Mouse parallax nudges the token (raycast → gentle force). Cursor is
a custom mono crosshair. A faint "scroll" glyph pulses at the bottom.

**Implementation.**
- Type-on with a mono `<Text>`; on complete, swap to an instanced particle burst
  that lerps to the token's centroid.
- Token = low-poly octahedron, `MeshTransmissionMaterial`, `distortion` driven by a
  `uTime` uniform; add `ChromaticAberration` (offset ~0.002) + light `Noise`.
- Idle bob via `Float`. Keep DOF focused on the token, background soft.

---

## ACT 2 — THE FAN-OUT (multi-domain search)
**Embodies:** *HUD / Sci-Fi FUI* + *Dimensional Layering*

**The story.** The engine wakes. Intelligence doesn't think in a line — it searches
five directions at once.

**What you see.** On scroll, the camera **pulls back hard** and the void reveals
itself as a vast 3D **lattice of 161 dim nodes** drifting in graphite fog — the rule
universe. From the token, **5 signal-blue beams** fire outward simultaneously
(product-match, style, palette, pattern, typography). Each beam races along the
lattice, and nodes it touches **light up and label themselves** in mono
(`#fintech`, `#glassmorphism`, `#WCAG-AA`, `#hero-centric`…). A live HUD readout in
the corner counts: `SEARCHING · 161 RULES · 5 DOMAINS`.

**Camera & motion.** Dolly back + slow orbit so you feel the lattice's depth. Beams
animate via a GLSL scan (a bright head + fading trail along each path).

**Interaction.** Hovering a lit node pops a tiny mono tooltip (its rule). Scroll
speed controls how fast the beams propagate — *you're driving the search*.

**Implementation.**
- 161 nodes as one `<Instances>` set; store target positions in an array; animate
  emissive intensity per-instance when a beam "arrives" (precompute beam→node hit
  times).
- Beams = tube geometry + scrolling UV shader (head glow + alpha trail).
- Cap lit labels to ~12 on screen (billboarded `<Text>`), fade the rest, so it reads
  as *intelligent selection*, not clutter.

---

## ACT 3 — IGNITION (the reasoning core / BM25 ranking)
**Embodies:** *Aurora Evolved* (used as a glow, not a gradient wall) + *Cyberpunk UI*

**The story.** Candidates collide and get *ranked*. This is the one hot moment.

**What you see.** The 5 beams snap back into the token, which **ignites** — the only
`--ember` in the whole site. A swirling cloud of candidate **style-shards** orbits it;
then they **sort in real time into a vertical ranked stack** (the BM25 cascade): the
winner locks at top with a confident *clack*, losers dim and fall away. Mono readout:
`RANKING · Soft UI Evolution ▸ 0.94`. Bloom blooms; a low sub-bass hit lands on the
lock. Chromatic aberration spikes for 200ms, then *settles* — the visual promise that
chaos is about to become order.

**Camera & motion.** Push IN toward the core on ignition, tiny shake on the lock,
then exhale back. Ember light spills across nearby nodes, then cools to signal-blue.

**Interaction.** Optional: a small prompt chip lets the user pick an industry
(`spa` / `fintech` / `gaming`); the ranked winner and downstream palette/type *change
accordingly* — a genuine micro-demo of the engine. (Powered by a tiny local lookup
seeded from the repo's rule table — no backend needed.)

**Implementation.**
- Style-shards = instanced thin planes; animate from orbit → sorted Y positions with
  staggered GSAP eases.
- Drive `Bloom.intensity` and `ChromaticAberration.offset` off a single
  `ignition` value (0→1→0). Ember is a point light enabled only here.
- Gate the audio behind first user interaction; honor reduced-motion (no shake).

---

## ACT 4 — CRYSTALLIZATION (complete design system output)
**Embodies:** *Bento Box Grid* + *Liquid Glass*

**The story.** The system precipitates out of the noise. This is the money shot.

**What you see.** The ranked winner's tokens **fly outward and snap into place** as a
floating 3D **bento board**: a palette bar (the chosen swatches tile in one by one), a
type-pairing card (display + mono lock together with a satisfying kern-snap), a
spacing/radius scale, and 2–3 ghost component cards (button, card, input) that
assemble from wireframe → frosted glass. The jittering Token from Act 1 is now
**faceted, still, and crowned** with the new palette — it resolved. Heading in bone
grotesk: **"From a sentence to a system."**

**Camera & motion.** Camera rises to a clean 3/4 "hero product" angle on the bento
board; everything decelerates into stillness (the calm payoff after Act 3's heat).

**Interaction.** Hover any bento tile → it lifts on Z with a soft glass refraction and
reveals its mono spec (`--primary #E8B4B8`, `Cormorant / Montserrat`, `radius: 16`).
Click the palette → swatches copy to clipboard. Drag-rotate the whole board slightly.

**Implementation.**
- Tiles = instanced rounded boxes; `MeshTransmissionMaterial` for the liquid-glass
  cards; stagger their snap with spring physics (`@react-spring/three`).
- Wireframe→solid via a dissolve shader (animate an edge-threshold uniform).
- This whole act can run on a JSON "design system" object so swapping the Act-3
  industry choice re-themes Act 4 live.

---

## ACT 5 — THE WALL OF 67 (the style library)
**Embodies:** *Chromatic Aberration / RGB Split* + *Parallax Storytelling*

**The story.** This was one of 67 possible worlds.

**What you see.** Camera glides sideways into an enormous, gently curved **wall of 67
floating panes**, each a living micro-preview of a style (Glassmorphism, Brutalism,
Claymorphism, Cyberpunk, Bento, Y2K, Vaporwave…). Distant panes blur and split into
RGB fringes; the centered pane snaps crisp. A mono ticker reads
`67 STYLES · 161 PALETTES · 57 PAIRINGS · 15 STACKS`.

**Camera & motion.** Horizontal rail dolly with parallax depth layers; subtle barrel
curve so it wraps the viewer. Chromatic aberration scales with distance from center.

**Interaction.** Scroll/drag rails the wall; the focused pane scales up and its style
name + "best for" tag fade in. Click a pane → it flies forward and momentarily
**re-skins the page chrome** (cursor, labels, accent) into that style for ~2s — a
playful proof of range.

**Implementation.**
- 67 panes as `<Instances>` with a texture atlas of preview thumbnails (KTX2);
  per-instance UV offset selects the thumbnail.
- Focus detection by nearest-to-center; drive a per-pane `focus` attribute for
  scale + de-aberration.
- Keep only the focused pane's preview at full res; others sampled from the atlas.

---

## ACT 6 — LIVING PROOF (interactive component)
**Embodies:** *Micro-interactions* + *3D Product Preview*

**The story.** Stop watching. Touch it.

**What you see.** The camera settles on **one real, fully-interactive UI component**
floating in 3D — say a pricing card or a booking widget — built with the exact tokens
from Act 4. It's not a video; it's live DOM composited into the scene (or a crisp
high-fidelity 3D-rendered UI). Light rakes across it on hover. Caption:
**"Generated by the rules you just watched fire."**

**Camera & motion.** Locked hero framing, slow idle float, gentle rim light tracking
the cursor.

**Interaction.** Real hover/focus/click states (150–300ms transitions — straight from
the repo's pre-delivery checklist). Toggle light/dark to show the token system holds
contrast. This act is the trust close.

**Implementation.**
- Use drei `<Html transform occlude>` to mount a real React component onto a 3D
  plane, OR render an offscreen DOM-to-texture. DOM route keeps it genuinely
  interactive and accessible.
- All states use the Act-4 token JSON so it's provably consistent.

---

## ACT 7 — INSTALL (CTA)
**Embodies:** *Minimalism & Swiss Style* + *Kinetic Typography*

**The story.** Now go build your own.

**What you see.** Everything calms to near-void. The faceted, crowned Token returns,
centered and serene. Below it, two crisp commands type themselves in mono — the real
install lines:
```
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
npm install -g uipro-cli
```
A single signal-blue CTA: **"Reason your design system →"**. Secondary links (GitHub
stars, docs, uupm.cc). Footer in quiet mono.

**Camera & motion.** Slow pull-back to a respectful distance; the token does one final
calm rotation and the palette crown glints. Loop-ready: the void here matches Act 1's
void, so the experience can quietly restart.

**Interaction.** Click-to-copy on each command (toast: `copied`). CTA hover = subtle
magnetic pull + ember flicker (the only callback to Act 3's heat).

**Implementation.** Mostly DOM over a calm canvas; cheap to render so the page ends
light and the CTA is instantly responsive.

---

## Scroll choreography (single timeline, 0→1)

| Offset | Act | Camera | Signature effect |
|--------|-----|--------|------------------|
| 0.00–0.12 | 1 Arrival | locked, shallow DOF | type-shatter, glitch token |
| 0.12–0.30 | 2 Fan-out | dolly back + orbit | 5 GLSL search beams |
| 0.30–0.45 | 3 Ignition | push in + settle | ember bloom, BM25 sort, AB spike |
| 0.45–0.62 | 4 Crystallize | rise to 3/4 hero | bento snap, wireframe dissolve |
| 0.62–0.80 | 5 Wall of 67 | horizontal rail | RGB-split parallax |
| 0.80–0.92 | 6 Living Proof | locked hero | real interactive component |
| 0.92–1.00 | 7 Install | pull back, loop | calm close, click-to-copy |

Drive a master `t = useScroll().offset`; each act reads its local progress
(`smoothstep(start,end,t)`), so motion never hard-cuts.

---

## Performance & accessibility (build it in, not after)

- **Instancing everywhere** (161 nodes, 67 panes) — one draw call per field.
- **Mount acts lazily**: only the active ± 1 act's heavy meshes are in the scene
  (gate by scroll range); dispose the rest.
- **Texture atlas + KTX2** for previews; **Draco** for the token/component glb.
- **`prefers-reduced-motion`**: kill camera shakes, the Act-3 AB spike, and auto-bob;
  replace beam animation with a static lit lattice. Site still tells the story, calmly.
- **Non-3D fallback (mandatory):** a fully crawlable, scroll-snapped 2D version — the
  same 7 beats as flat sections with CSS chromatic-split + the real copy, headings,
  install commands, and component. Ship real text in the DOM (never trapped in canvas)
  for SEO. Detect WebGL/low-power and serve this automatically.
- **Mobile:** reduce node count (161→~60 visible), disable DOF, halve bloom, swap the
  Act-5 rail for a swipeable card stack. Test on a mid-range phone, not just a laptop.
- Budget: hero+lattice under ~2–3MB compressed; first meaningful paint before WebGL
  boots.

---

## Asset list

- **Create:** token glb (faceted + raw variants), 67 style preview thumbnails (atlas),
  one hero component (Act 6), GLSL for beam-scan + crystallize-dissolve, 1 sub-bass +
  1 lock SFX.
- **From repo (free):** the example prompt, the 4-stage pipeline, the real numbers
  (161/67/57/15/24/99), the rule/palette/type data for the live industry demo, the
  install commands, the anti-pattern list (drives the no-purple constraint).
- **Source:** 2 fonts (display grotesk + mono) via Google Fonts.

---

## Build order (so it's shippable, not just dreamy)

1. **Scroll skeleton** — Lenis + R3F `ScrollControls`, 7 empty acts, camera rig on
   the master timeline. Prove the journey with placeholder cubes first.
2. **Token + Act 1/7** — the hero motif and the calm close (your strongest first
   impression and your conversion, bookended).
3. **Lattice + beams (Act 2)** — instancing + the beam shader (your signature wow).
4. **Crystallization (Act 4)** — the bento payoff; wire the design-system JSON.
5. **Ignition (Act 3)** — connect Act 2→4 with the ember moment + ranking.
6. **Wall of 67 (Act 5)** + **Living Proof (Act 6)**.
7. **Postprocessing pass, perf pass, fallback, mobile.** Then polish micro-interactions
   to the repo's 150–300ms checklist.

---

## Optional stretch ideas

- **Make the Act-3 industry picker real**: seed a tiny client-side index from the
  repo's rule CSVs so choosing "fintech" vs "spa" genuinely re-reasons palette + type
  + pattern downstream. The site becomes a live mini-uupm — the ultimate proof.
- **Cursor leaves a faint token-trail** that snaps to the lattice grid (reinforces
  "your intent moving through the engine").
- **Konami-style easter egg**: type a prompt anywhere and watch a fast-forward run of
  all 7 acts resolve to a bespoke system.
