# Animation & Technique Reference

The vocabulary for the plan's **Motion & animation system** section. Use it to make
motion recommendations concrete (real library names, real techniques, rough budgets)
instead of vague ("add some 3D animations"). Verify specifics with `web_search` when a
client's target effect is unusual — this field moves fast. Budgets are planning rules
of thumb, not hard limits; they shift with the target devices.

## Rendering engine — pick per client

| Tool | Use when | Notes |
|---|---|---|
| **Three.js** | Custom, art-directed 3D; maximum control. | The award-tier default (igloo.inc). Steep curve. |
| **React Three Fiber (R3F) + drei** | Same power inside React/Next; declarative, huge helper ecosystem. | The standard for most studio production today. drei gives cameras, loaders, `MeshTransmissionMaterial`, `Environment`, `Instances`, `Html`, `ScrollControls`. |
| **WebGPU + TSL** | New high-end builds wanting compute (particles/fluids), heavy draw calls. | Production-ready since Three.js r171; auto WebGL2 fallback (~95% coverage). TSL shaders compile to both WGSL & GLSL. Verify device support per project. |
| **Spline** | No-/low-code, rapid prototyping, simple hero scenes, tight budget/timeline. | The "3D-lite" option; exports to R3F. Watch runtime weight; limited fine control. |
| **Babylon.js / PlayCanvas** | Batteries-included engine apps; collaborative editor (PlayCanvas). | Less common in the creative-agency award tier. |
| **Unreal + Pixel Streaming** | Photoreal fidelity that can't run in-browser (configurators, showrooms). | Server-renders, streams video; high infra cost + latency. Niche. |

Heuristic: **Three.js/R3F** = custom award-tier · **Spline/3D-lite** = fast/affordable
· **hybrid** (R3F shell + Spline/baked assets) = middle ground · **Unreal stream** =
only when fidelity demands it and budget allows. (Cross-check `3d-stack-selection.md`.)

## Scroll & motion — the canonical award-site stack

**Lenis (smooth scroll) + GSAP/ScrollTrigger (timeline + scrub) + R3F/drei (3D) +
Framer Motion (DOM/UI).** Swap in **Theatre.js** when camera choreography is complex.

- **Lenis** — normalizes/eases native scroll; the near-universal base layer.
- **GSAP + ScrollTrigger** — dominant timeline/scrub engine; pin sections, scrub
  timelines. Wire **Lenis into GSAP's ticker** and drive ScrollTrigger from Lenis —
  never run two scroll systems. (GSAP incl. all plugins is now free.)
- **Driving 3D from scroll** — animate **shader uniforms** and **camera
  position/rotation** from a normalized scroll progress (0→1). The core cinematic move.
- **drei `ScrollControls` / `useScroll`** — R3F-native scroll progress for R3F-only builds.
- **Theatre.js** (`@theatre/r3f`) — visual keyframe sequencer for hand-authored camera
  fly-throughs; powerful but adds tooling overhead.
- **Framer Motion** — for the DOM/UI layer (nav, text, page transitions), not the scene.

## Shaders, materials, post-processing

- **GLSL custom shaders** (or **TSL** on WebGPU) — the signature of top-tier work:
  vertex displacement, noise/gradient materials, dissolve/reveal. igloo's look is
  custom-shader + particle driven.
- **drei `MeshTransmissionMaterial`** — the go-to premium glass/liquid/crystal material;
  built-in chromatic aberration, roughness blur, sees other transmissive objects.
- **Post-processing** (`@react-three/postprocessing`): **Bloom** (selective — lift
  colors above 1.0, set `luminanceThreshold`), **ChromaticAberration**,
  **DepthOfField**, **Noise/Grain**, **Vignette**, **Glitch**. Merge into few passes.
- **Particle systems** — `Points` + custom shaders; positions via **GPGPU** (FBO
  ping-pong on WebGL, **compute shaders** on WebGPU/TSL). Basis of morphs and fluids.
- **Instancing** — `InstancedMesh` / drei `<Instances>` for repeated geometry; cuts
  draw calls 90%+. Non-negotiable for node fields, galleries, particle grids.

## Assets & optimization

- **glTF / GLB** standard; GLB (binary) for production.
- **Draco** geometry compression — any model >1MB. (Shrinks file size, *not* triangle
  count — over-heavy meshes must be simplified, not just compressed.)
- **Meshopt** — comparable/better ratios, faster decode; gaining adoption.
- **KTX2 / Basis** GPU textures — stay compressed in VRAM (~4–10× less memory). UASTC
  for hero/normal maps, ETC1S for secondary/environment textures.
- **gltf-transform** CLI = the optimization pipeline (`inspect` → Draco/meshopt + KTX2);
  **gltfjsx** generates R3F components from GLB.
- **Rough budgets** (broad device support): hero object ~50k–100k tris · props ~0.5k–5k
  tris each · whole scene <~500k tris · **draw calls <100/frame desktop, <50 mobile** ·
  active lights ≤3. **LOD** (`THREE.LOD`) for distance detail. **Lazy-mount** heavy
  scenes on scroll-into-view; `frameloop="demand"` for static scenes. Always
  `dispose()` on unmount; never allocate inside `useFrame`.

## Loading UX

- **Preloader** that pre-warms (compiles shaders, uploads textures) before reveal;
  drei `useProgress` drives a %. Balance against perceived speed.
- **Suspense** — `useGLTF`/`useTexture` suspend; **drei `<Preload all />`** warms GPU.
- **Progressive enhancement** — ship real HTML first, layer WebGL on top (helps load,
  crawlability, and gives a baseline if WebGL fails).
- **Asset streaming** — load hero scene first; lazy-load later sections on approach;
  low-res → high-res texture swaps.

## Performance & device strategy

- **FPS:** 60 desktop · ~30 cap on mobile (saves battery, avoids thermal throttle).
- **Mobile fallback recipe:** clamp DPR to ~[1, 2], disable/limit shadows, halve
  texture res, KTX2 everywhere, draw calls <50, fewer particles, simpler/disabled
  post-processing; provide a static image/video poster for low-end devices.
- **`prefers-reduced-motion`** — disable scroll-jacking/auto-motion, freeze/simplify
  the scene. Must be handled manually in WebGL.
- **WebGL/WebGPU detection** — feature-detect; serve image/video/HTML fallback if
  unsupported (`three/webgpu` falls back to WebGL2 automatically).
- **SEO** — text in `<canvas>` is invisible to crawlers/screen readers. Keep real
  copy/headings in the DOM (overlaid or via drei `<Html>`); treat canvas as decoration.
  *(This is exactly the tradeoff igloo accepted — see `north-star-igloo.md`.)*
- **Bundle** — code-split / dynamic-import the Canvas; keep above-the-fold JS lean.

## Signature effects → how they're built

- **Scroll-scrubbed camera path** — normalize scroll (Lenis) → drive camera along a
  `CatmullRomCurve3`/keyframes via GSAP/ScrollTrigger (or Theatre.js / drei useScroll).
- **Material reveal / dissolve** — tween a shader uniform (noise threshold, clip plane,
  `mix()`) on scroll/hover; noise + smooth mask = liquid/organic edge.
- **Particle morph** — two target position buffers; lerp by a `progress` uniform in the
  vertex shader; GPGPU/compute for large counts. (igloo's per-link shape morph.)
- **Fluid / distortion** — GPGPU ping-pong or WebGPU compute fluid; or screen-space
  refraction/displacement on a fullscreen pass; cursor-driven ripple via velocity texture.
- **Text-to-3D shatter** — render text/image to particles, or fragment a mesh into
  instanced shards; explode via a transition uniform.
- **Magnetic cursor** — DOM eased toward pointer (GSAP `quickTo`); in 3D, raycast or a
  grid of instances rotating toward the pointer; custom cursor + trailing bloom shader.
- **Page transitions** — full-screen WebGL wipe (noise-masked reveal, RGB-split slide)
  over the route change; persistent Canvas across routes to avoid re-init; on DOM side,
  Framer Motion `AnimatePresence` or the View Transitions API.
- **Glass/crystal hero** — `MeshTransmissionMaterial` + `Environment` (HDRI/Lightformer)
  + selective Bloom + subtle chromatic aberration + DOF.

## Source-of-truth links to research deeper

- Codrops cinematic-3D-scroll & shader-with-GSAP tutorials — https://tympanus.net/codrops/
- drei docs — https://drei.docs.pmnd.rs/ · react-postprocessing —
  https://react-postprocessing.docs.pmnd.rs/
- Lenis — https://github.com/darkroomengineering/lenis · gltf-transform —
  https://gltf-transform.dev/
- Three.js forum (case studies & breakdowns) — https://discourse.threejs.org/
