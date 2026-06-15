# 3D Stack Selection

Pick the approach that fits *this* client. The most common mistake is reaching for
heavy custom WebGL when a lighter approach would ship faster, perform better, and be
maintainable. Match the choice to budget, brand ambition, content, performance/SEO
needs, and who maintains the site.

## The four approaches

### 1. Three.js / React Three Fiber (custom WebGL)
- **Best for:** distinctive brands, product configurators, signature interactive
  heroes, anything needing custom logic/physics/shaders.
- **Strengths:** maximum control and uniqueness; can be highly optimized.
- **Costs:** highest effort and skill; longest timeline; you own performance,
  loading, and cross-device QA.
- **Maintenance:** developer-dependent.
- **Pick when:** the brand justifies a custom moment AND there's budget/skill AND a
  developer will maintain it.

### 2. Spline (or similar no-code 3D)
- **Best for:** fast, beautiful 3D scenes without hand-writing WebGL; designer-led
  teams; quick pitches and prototypes.
- **Strengths:** rapid iteration; visual editor; easy export/embed; good for hero
  scenes and decorative 3D.
- **Costs:** less custom interactivity/logic; bundle/runtime size needs watching;
  some platform lock-in.
- **Maintenance:** designer-friendly — non-coders can update scenes.
- **Pick when:** speed and visual polish matter more than deep custom behavior, or a
  non-developer maintains it.

### 3. Hybrid (Spline/exported assets in a React/Three scene)
- **Best for:** pragmatic middle ground — author visuals in a no-code tool, wire
  interactions/data in code.
- **Strengths:** balances speed and control; reuse modeled assets; keep React
  ecosystem.
- **Costs:** two toolchains to manage; integration overhead.
- **Pick when:** you want custom interactivity but not from-scratch asset authoring.

### 4. 3D-lite (scroll/parallax/CSS-3D/subtle WebGL accents)
- **Best for:** when performance, SEO, budget, or accessibility dominate and full 3D
  would be overkill.
- **Strengths:** fast, cheap, robust, crawlable; still feels modern and dynamic.
- **Costs:** less "wow"; limited true 3D depth.
- **Pick when:** small budget, content/SEO-heavy site, regulated industry, or a
  conservative audience — depth comes from motion, not heavy 3D scenes.

## Decision factors
| Factor | Leans 3D-lite / Spline | Leans Hybrid / Three.js |
|---|---|---|
| Budget | Small | Healthy |
| Timeline | Tight | Flexible |
| Brand ambition | Conventional | Distinctive / premium |
| Custom interactivity | Low | High (configurator, physics) |
| Performance/SEO priority | Critical | Manageable with effort |
| Maintainer | Non-developer | Developer |
| Device/audience | Low-power, broad | Modern, capable |

## Always specify
- **Why this fits the client** — tie to Phase 2 findings, not preference.
- **Tradeoffs** accepted with the choice.
- **A fallback approach** if budget/timeline tightens (usually drop one tier:
  Three.js → Hybrid → Spline → 3D-lite).
- **A non-3D fallback experience** for low-power devices, reduced-motion users, and
  crawlers — non-negotiable on every build regardless of stack.

## Performance, SEO & accessibility (every approach)
- Lazy-load 3D below the fold; gate heavy scenes behind interaction or viewport.
- Set asset-weight ceilings (models, textures); compress (Draco/KTX2 where relevant).
- Honor `prefers-reduced-motion`; provide a static poster/fallback.
- Keep real content in HTML so it's crawlable; don't lock copy inside the canvas.
- Test on mid-range mobile early — not just a fast laptop.
