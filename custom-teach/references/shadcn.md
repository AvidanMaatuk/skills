# shadcn/ui reference (for explainer authoring)

Brings the shadcn/ui *look* and *motion* into self-contained HTML explainers **without** Tailwind, React, or a build step. Everything ships in `../assets/shadcn.css` (tokens + component surfaces + the tailwindcss-animate enter/exit keyframes + the Radix `data-state` open/close pattern). Token and animation values mirror shadcn/ui and tailwindcss-animate (both MIT).

Use this when the concept is **UI / interaction / state** — a component flipping open, a list revealing, a dialog appearing, progressive disclosure — and you want a clean, modern surface. For physics, 3D, scroll, or timeline sequencing, use CSS / `anime` / `zdog` / `gsap` instead.

Wire it up (standalone snippet → `../assets`; workspace explainer → `./assets`):

```html
<link rel="stylesheet" href="../assets/shadcn.css">
<body class="ui"> ... </body>   <!-- .ui sets the font + smoothing -->
```

Dark mode: add `class="dark"` (or `data-theme="dark"`) on a wrapper.

## Surfaces

| Class | What |
|---|---|
| `.ui-card` + `__header __title __desc __content __footer` | card |
| `.ui-btn` + `--secondary --outline --ghost --destructive` | button |
| `.ui-badge` + `--secondary --outline --destructive` | pill badge |
| `.ui-input` | text field |
| `.ui-separator` | hairline rule |
| `.ui-accordion` + `__item __trigger __chevron __content` | accordion |
| `.ui-overlay` / `.ui-dialog` | modal scrim + panel |

Tokens (HSL triplets, override on `:root` to re-theme): `--background --foreground --card --primary --secondary --muted --accent --destructive --border --input --ring --radius`. Use as `hsl(var(--primary))` or `hsl(var(--primary) / 0.9)`.

## Motion — tailwindcss-animate vocabulary

Compose `animate-in` **or** `animate-out` with one or more modifiers. This is the shadcn entrance/exit language.

```html
<div class="animate-in fade-in zoom-in duration-300">appears</div>
<div class="animate-in slide-in-from-bottom-8 fade-in">rises + fades in</div>
<div class="animate-out fade-out zoom-out">leaving</div>
```

- Fade: `fade-in` / `fade-out`
- Zoom: `zoom-in` / `zoom-in-50` / `zoom-out`
- Slide in: `slide-in-from-{top,bottom,left,right}` (+ `-8` for a larger 2rem offset)
- Slide out: `slide-out-to-{top,bottom,left,right}`
- Spin: `spin-in-90`
- Tune: `duration-{150,200,300,500,700}`, `delay-{100,200,300,500}`, `ease-{out,in,in-out}`, `fill-mode-forwards`
- Stagger a list/grid: wrap in `.ui-stagger`; children get incremental delays (8 steps). Combine with `animate-in fade-in slide-in-from-bottom` on the children.

## `data-state` pattern (the Radix way)

shadcn components animate by toggling `data-state="open" | "closed"` with JS. The CSS reacts:

```html
<button class="ui-accordion__trigger" data-state="closed" onclick="toggle(this)">…</button>
<div class="ui-accordion__content" data-state="closed"><div><div>…body…</div></div></div>
```

```javascript
function toggle(btn) {
  const open = btn.dataset.state === "open";
  const next = open ? "closed" : "open";
  btn.dataset.state = next;
  btn.nextElementSibling.dataset.state = next;   // content
}
```

Accordion height animates via a CSS grid `0fr → 1fr` trick (no measuring JS). Dialog/overlay fade+zoom in on `open`, reverse on `closed` — keep the node in the DOM through the close animation, then hide it.

## Accessibility

`shadcn.css` already disables all of the above under `@media (prefers-reduced-motion: reduce)`. Keep triggers as real `<button>`s and label dialogs.
