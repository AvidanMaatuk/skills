# GSAP reference (for explainer authoring)

Condensed from the official [GSAP skills](https://github.com/greensock/gsap-skills) (greensock, MIT) — core, timeline, ScrollTrigger, utils, accessibility. Read this **before creating a GSAP snippet** so the animation is correct and fast to write. GSAP 3.13 is fully free, all plugins included.

Bundled assets (reference by relative path; ScrollTrigger optional):

```html
<script src="../assets/gsap.min.js"></script>          <!-- standalone snippet -->
<script src="../assets/ScrollTrigger.min.js"></script>
<!-- inside a workspace explainer the path is ./assets/... -->
```

## When GSAP is the right tool (vs CSS / anime.js)

Reach for GSAP when the concept needs **runtime control** (pause / reverse / seek / scrub), **precise multi-step sequencing**, **scroll-linked** reveal, complex easing, or values computed in JS. For a single static state flip, CSS transitions are still lighter — don't pull in GSAP for decoration.

| Teaching need | API |
|---|---|
| Sequence / pipeline / accumulation over time | `gsap.timeline()` + position parameter |
| Reveal-as-you-scroll, scrubbed process, pin-and-explain | `ScrollTrigger` |
| Staggered set (grid, list, particles) | `stagger` |
| Entrance of a diagram element | `gsap.from(... autoAlpha)` |
| Build-up of an SVG diagram (line draws itself) | tween `strokeDashoffset` |
| Overshoot / springy emphasis | `ease: "back.out(1.7)"` / `"elastic.out"` |

## Core tweens

- `gsap.to(targets, vars)` — animate to `vars` (most common)
- `gsap.from(targets, vars)` — animate from `vars` to current (entrances)
- `gsap.fromTo(targets, fromVars, toVars)` — explicit start + end
- `gsap.set(targets, vars)` — apply instantly (duration 0)

Targets: selector string, element, array, or NodeList.

Common vars: `duration` (s, default .5), `delay`, `ease` (default `"power1.out"`), `stagger`, `repeat` (`-1`=infinite), `yoyo`, `onComplete/onStart/onUpdate`, `overwrite` (`false`|`true`|`"auto"`).

**Transforms — use GSAP aliases, not the raw `transform` string:** `x`,`y`,`z` (px), `xPercent`,`yPercent`, `scale`/`scaleX`/`scaleY`, `rotation` (deg), `rotationX`,`rotationY`, `skewX`,`skewY`, `transformOrigin`. Relative: `x:"+=20"`. Directional rotation suffix: `"-170_short"`, `"+=30_cw"`.

`autoAlpha` — prefer over `opacity` for fade in/out (also toggles `visibility`, so hidden elements don't catch clicks). Can animate CSS vars (`"--hue": 180`).

```javascript
gsap.to(".box", { x: 100, rotation: "360_cw", duration: 1, ease: "power2.out" });
gsap.from(".card", { autoAlpha: 0, y: 24, stagger: 0.1, duration: 0.6 });
```

## Easing

String eases unless a custom curve is needed: `power1..power4`, `back`, `bounce`, `circ`, `elastic`, `expo`, `sine`, each with `.in`/`.out`/`.inOut`; `"none"` = linear. Overshoot: `"back.out(1.7)"`. Spring: `"elastic.out(1, 0.3)"`.

## Timelines (sequencing)

```javascript
const tl = gsap.timeline({ defaults: { duration: 0.5, ease: "power2.out" } });
tl.to(".a", { x: 100 })
  .to(".b", { y: 50 }, "+=0.2")   // 0.2s after previous end
  .to(".c", { opacity: 0 }, "<"); // start with previous
```

Position parameter (3rd arg): absolute `1`; relative `"+=0.5"` / `"-=0.2"`; label `"intro"` / `"intro+=0.3"`; `"<"` = previous start, `">"` = previous end (default); `"<0.2"` = 0.2s after previous start.

Labels: `tl.addLabel("outro", "+=0.5")`, `tl.play("outro")`. Nest: `master.add(childTl, 0)`. Control: `.play() .pause() .reverse() .restart() .time(2) .progress(.5) .kill()`. Options: `paused:true`, `repeat`, `yoyo`, `defaults`.

**Prefer timelines over chaining with `delay`.**

## ScrollTrigger (scroll-linked teaching)

```javascript
gsap.registerPlugin(ScrollTrigger);
gsap.from(".step", {
  autoAlpha: 0, y: 40, stagger: 0.2,
  scrollTrigger: { trigger: ".steps", start: "top 75%", toggleActions: "play none none reverse" }
});
```

`start`/`end` = `"triggerPos viewportPos"` (e.g. `"top center"`, `"bottom 80%"`), or px / `"+=300"`. Key opts: `scrub` (`true` or seconds — ties progress to scroll), `pin:true` (pin while active — good for "pin and explain"), `toggleActions` (onEnter onLeave onEnterBack onLeaveBack), `markers:true` (dev only), `once`. Attach ScrollTrigger to the **timeline**, not child tweens. Pick **either** `scrub` **or** `toggleActions`. `ScrollTrigger.batch(".item", { onEnter: els => gsap.to(els,{autoAlpha:1, stagger:.15}) })` for reveal-on-scroll lists.

## Utils

`gsap.utils.clamp(min,max,v)`, `mapRange(inMin,inMax,outMin,outMax,v)`, `interpolate(a,b,t)`, `random(min,max[,step])`, `snap(step,v)`, `wrap(min,max,v)`, `toArray(sel)`.

## Accessibility / responsive — `gsap.matchMedia()`

```javascript
const mm = gsap.matchMedia();
mm.add({ isDesktop: "(min-width:800px)", reduce: "(prefers-reduced-motion: reduce)" }, (ctx) => {
  const { isDesktop, reduce } = ctx.conditions;
  gsap.to(".box", { rotation: isDesktop ? 360 : 180, duration: reduce ? 0 : 2 });
});
```

Animations created in a matching block auto-revert when it stops matching. **Always honour `prefers-reduced-motion`** in explainers (set `duration:0` or skip).

## Do / Don't

- ✅ camelCase props; transform aliases over raw `transform`; `autoAlpha` over `opacity`; timelines over `delay`; store the returned tween/timeline when you need control.
- ❌ animate `width`/`height`/`top`/`left` when `x`/`y`/`scale` work; `markers:true` left in; `scrub`+`toggleActions` together; ScrollTrigger on child tweens; stacking `from()`/`fromTo()` on the same prop without `immediateRender:false` on the later ones.
