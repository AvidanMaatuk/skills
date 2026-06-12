# Animation Library Index

Every snippet in this directory is a single self-contained HTML file — no external dependencies, openable directly in a browser. Before creating any animation for an explainer, search this index first: **reuse → modify → create**, in that order. Anything you create or meaningfully modify must be saved back here and added to this table (see [ANIMATIONS-FORMAT.md](../ANIMATIONS-FORMAT.md)).

## Pedagogical uses

- **process** — shows progression, steps, accumulation, or pipelines over time
- **spatial** — 3D structure, geometry, orbital/mechanical models
- **motion** — physics and motion concepts: easing, oscillation, waves, collisions
- **state** — a system flipping between discrete states; toggles and switches
- **emphasis** — drawing the eye to a key term or moment; use sparingly
- **exercise** — interactive widgets the user manipulates; feedback-loop material
- **diagram** — animated data or concept relationships
- **hook** — illusions and curiosities that open a session or spark a question
- **reward** — small delights for completed exercises; budget-limited

## Index

| File | Use | Library | Description |
|---|---|---|---|
| 005-sleek-sliding-toggle-checkbox.html | state | css | Sliding on/off toggle; binary state change with smooth transition |
| 007-3d-text-marquee-effects.html | spatial | css | Text rotating on a 3D cylinder; perspective and transform-style |
| 008-charging-loader-animation.html | process | css | Battery-charging fill; accumulation toward completion |
| 012-broken-text-effects.html | emphasis | css | Text that fractures apart; destructive change, irreversibility |
| 013-hot-coffee-cup.html | reward | css | Steaming coffee cup; break/completion moment |
| 014-three-languages-for-web-development.html | diagram | css | HTML/CSS/JS role cards; tri-partite concept split |
| 015-development-skills-card.html | diagram | css | Animated skill-level bars; proportions and comparison |
| 020-pixel-animation-heart-shape.html | reward | js | Heart drawn pixel-by-pixel; grid construction, also for raster concepts |
| 024-waves.html | motion | css | Layered sine waves; periodicity, phase offset |
| 028-penrose-triangle.html | hook | css | Impossible triangle; geometry/perception opener |
| 031-minimalist-ping-pong-animation.html | motion | css | Ball bouncing between paddles; back-and-forth exchange (request/response) |
| 036-solar-eclipse.html | spatial | css | Moon passing over sun; occlusion and alignment |
| 042-equalizer-loader.html | process | css | Bouncing equalizer bars; parallel fluctuating quantities |
| 046-bounced-ball-effect.html | motion | css | Ball bounce with squash; easing and energy loss |
| 050-newtons-cradle.html | motion | css | Newton's cradle; momentum/energy transfer through a chain |
| 053-text-fade-loader.html | process | css | Text characters fading in sequence; sequential processing |
| 055-sun-earth-and-moon-model.html | spatial | css | Orbiting earth and moon; nested rotation frames, hierarchy |
| 060-lego-brick.html | spatial | css | 3D lego brick; composition from faces |
| 077-wavy-flag.html | motion | css | Flag ripple; wave propagation across a surface |
| 080-bicycle-wheel.html | spatial | css | Spinning spoked wheel; rotation, angular structure |
| 083-a-ball-climbing-the-stairs.html | process | css | Ball hopping up stairs; discrete incremental progress |
| 085-bouncing-ball.html | motion | css | Plain gravity bounce; baseline easing demo |
| 091-train-loader.html | process | css | Train crossing screen; pipeline / transport metaphor |
| 092-saturn.html | spatial | css | Saturn with tilted rings; inclined planes in 3D |
| 100-shimmering-neon-text.html | emphasis | css | Neon flicker on a key word; spotlight a term |
| 101-pendulums.html | motion | css | Pendulum row with phase shift; oscillation, frequency, interference patterns |
| 104-truck-loader.html | process | css | Truck hauling progress; payload transfer |
| 116-online-status-detector.html | state | js | Live online/offline event listener; event-driven state, real browser API |
| 118-hourglass-loader.html | process | css | Flipping hourglass; elapsing time, reset cycles |
| 127-circle-illusion.html | hook | css | Dots in line look like rotating circle; decomposition of circular motion |
| 129-stripe-illusion.html | hook | css | Moving stripe illusion; perception vs reality opener |
| 137-abstract-water-wave-animation.html | motion | css | Organic blob waves; fluid, continuous deformation |
| 138-iphone-price-comparison-chart.html | diagram | css | Animated bar chart with values; quantitative comparison |
| 140-text-fade-in-effect.html | emphasis | css | Staggered word reveal; pacing a sentence or definition |
| 145-power-switch.html | state | css | Power button with glow; on/off with visual feedback |
| 152-black-dots-illusion.html | hook | css | Vanishing dots grid illusion; attention/perception opener |
| 153-emoji-tooltips.html | exercise | js | Hover/tap tooltips; reveal-on-demand annotations for labeled diagrams |
| 156-airplane-window-toggle.html | state | css | Window shade slides day/night scene; state with rich consequences |
| 157-chessboard-illusion.html | hook | css | Checker-shadow style illusion; context-dependence of perception |
| 158-umbrella-toggle.html | state | css | Umbrella opens, rain starts; cause-and-effect toggle |
| 167-two-hearts.html | reward | css | Two hearts beating; warm completion moment |
| 171-snowflake.html | reward | css | Falling snowflakes; ambient celebratory backdrop |
| 174-calendar.html | exercise | js | Live calendar that renders current month from `Date`; date logic playground |
| 176-relationship-between-html-css-js.html | diagram | js | Interactive HTML/CSS/JS relationship explainer; layered web-stack model |
| 178-tile-pattern-designer.html | exercise | js | Click-to-design tile pattern grid; user constructs, instant visual feedback |
| gsap-timeline-pipeline-sequence.html | process | gsap | Stages light up in dependency order along a pipeline; sequential processing, ordered stages |
| gsap-scroll-reveal-steps.html | process | gsap | Steps reveal (and reverse) as you scroll — scrollytelling; reader-paced sequence, accumulation |
| gsap-svg-draw-build.html | diagram | gsap | SVG diagram draws itself node-by-node, edges between them; construction / build order of a structure |
| gsap-stagger-grid-from-center.html | emphasis | gsap | Grid cells scale in staggered from the centre; reveal wave propagating from a source |
| shadcn-accordion-progressive-disclosure.html | exercise | shadcn | Accordion opens one panel at a time; progressive disclosure, hierarchy, reveal-on-demand |
| shadcn-card-stagger-reveal.html | emphasis | shadcn | Cards fade + slide in with staggered delay; grouped entrance, pacing a set of items |
| shadcn-dialog-state.html | state | shadcn | Dialog + scrim open/close on one flag; discrete state with rich, coordinated consequences |

## Libraries available to new snippets

New snippets may also use the bundled libraries in `../assets/` (copy the relevant file reference when embedding in a workspace explainer):

- `anime.min.js` — timelines, staggering, SVG morphing; lightweight JS animations
- `gsap.min.js` (+ `ScrollTrigger.min.js`) — runtime-controllable timelines, staggers, scroll-linked reveal, springy/elastic eases; first choice for **sequencing, scroll-driven, or controllable** JS animation. Read [`../references/gsap.md`](../references/gsap.md) before authoring.
- `zdog.dist.min.js` — round, designer-friendly 3D models; first choice for **spatial** concepts
- `shadcn.css` — shadcn/ui tokens + component surfaces (card, button, badge, accordion, dialog) + tailwindcss-animate enter/exit classes and the `data-state` pattern; first choice for **UI / interaction / discrete-state** concepts that want a clean modern surface. Read [`../references/shadcn.md`](../references/shadcn.md).
- `animate.min.css` / `magic.min.css` — ready-made CSS entrance/attention classes for **emphasis**
- `lottie_light.min.js` — plays downloaded `.json` Lottie files (playback only; store the `.json` next to the snippet and record it in this index)

> GSAP and shadcn snippets reference their bundled library by relative path (`../assets/gsap.min.js`, `../assets/shadcn.css`) instead of inlining — see the packaging note in [ANIMATIONS-FORMAT.md](../ANIMATIONS-FORMAT.md).
