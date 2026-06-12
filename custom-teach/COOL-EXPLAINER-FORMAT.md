# Cool Explainer Format

An **opt-in** explainer style for the teaching skill: a single, self-contained HTML
lesson with a signature look (boot-up intro, neon blueprint surface, scroll-staged
sections), heavy-but-earned animation, hand-built interactive simulations, and a
quiz that scores itself. It is a *skin and a structure* layered on top of the normal
explainer guidance in [SKILL.md](./SKILL.md) — same pedagogy (mission-grounded,
glossary-true, citation-backed), a much bolder delivery.

A working skeleton lives next to this file: [`cool-explainer-template.html`](./cool-explainer-template.html).
**Start from it.** It already wires the boot sequence, progress bar, side-nav,
scroll-reveal, flip cards, quiz engine, confetti, and one example simulation. Copy it
into the workspace, reskin the tokens, and replace the stages.

## When to use it (and when not to)

Use this format **only when the user explicitly asks for it** — phrases like
"make it cool", "the cool format", "cool explainer", "do it in the cool style", or a
`/custom-teach … cool` style request. Default explainers follow [SKILL.md](./SKILL.md) as
usual; this format is never the silent default.

Once the user has asked for it in a workspace, treat it as **sticky for that topic**:
later explainers in the same workspace keep the format unless the user says otherwise.
Keep a one-line note in `CURRICULUM.md` (or a learning record) that the workspace runs
in cool format, so future sessions stay consistent.

## Non-negotiables

1. **One self-contained HTML file.** Inline all CSS and JS. Only external dependency
   allowed: Google Fonts. It must open and fully work from `file://`, offline. No
   build step, no module imports, no `fetch`.
   *(If a concept genuinely needs a bundled library from the skill's reuse ladder —
   GSAP for scroll choreography, zdog for 3D — you may wire `./assets/…` per
   [ANIMATIONS-FORMAT.md](./ANIMATIONS-FORMAT.md). Most cool-format sims are plain
   CSS/JS and need nothing.)*
2. **Direction & language follow the learner.** Set `<html lang dir>` correctly —
   `dir="rtl"` for Hebrew/Arabic. Wrap every technical/foreign term in a `.term` chip
   (it forces `direction:ltr` inside RTL prose). Use logical CSS (`border-inline-start`,
   `text-align:start`) so it mirrors cleanly.
3. **Active learning, not a poster.** Every concept that involves motion, sequence,
   state, or comparison earns an interactive **sim**. Minimum **3 sims** per lesson,
   plus a checkpoint quiz after most stages and a scored final quiz. Reading without
   doing is a failure of the format.
4. **Animation is earned.** Animate the concept (data flow, a state transition, a
   comparison), or celebrate success (confetti). Never animate as decoration. The
   page-load reveal and one signature flourish are the only "free" motion.
5. **Faithful + cited.** Cover the source material completely (don't drop a concept to
   look clean). Keep the skill's citation rule: back claims with links, placed in
   `.callout` blocks or a resources strip. Adhere to `GLOSSARY.md` for every term.
6. **Honour `prefers-reduced-motion`.** The template already does; keep it.

## Visual identity

The default skin is a **dark blueprint console**: night background, faint grid +
glow + scanlines, electric-cyan primary with hot-amber emphasis, a heavy display
face over a clean body face, monospace for anything technical. This is the reference
"Kernel Space" theme baked into the template.

**Reskin per topic — change the skin, keep the structural DNA.** Pick a bold direction
that fits the subject (the skill's frontend-aesthetic rule: commit hard, avoid generic
AI looks — no Inter/Roboto, no purple-on-white). Edit only the `:root` tokens, the two
Google Fonts, and the `body::before/after` atmosphere. Keep the boot overlay, staged
reveal, sim shell, and quiz engine intact.

### Tokens to set (copy from the template's `:root`)

```
--bg / --bg-2 / --panel / --panel-2   surfaces (commit to light OR dark)
--line                                hairline borders
--ink / --muted                       text
--accent  (+ --accent-soft)           primary — "subject A" in sims
--amber   (+ --amber-soft)            emphasis — "subject B" / highlights
--good / --bad / --violet             success / error / quiz + waiting
--font-display / --font-body / --font-mono
--glow-accent / --glow-amber          neon shadows
```

Keep the **semantic colour roles** stable even when you change the hues: one primary,
one emphasis, plus fixed success/error so the sims and quizzes read consistently.

### Theme starting points

| Subject mood | display / body | surface | accent / emphasis |
|---|---|---|---|
| systems, networks, low-level (default) | Suez One / Heebo | dark navy | cyan / amber |
| biology, chemistry, nature | Fraunces / Nunito Sans | warm off-black | lime / coral |
| history, law, literature | Playfair Display / Newsreader | parchment light | ink-blue / oxblood |
| math, physics, abstract | Space Grotesk *(avoid if overused)* / IBM Plex Sans | near-black | violet / teal |
| retro / games / hardware | Orbitron / Chakra Petch | CRT black | magenta / lime |

## Page structure (fixed order)

The template ships this skeleton; keep the order, vary the content.

1. **Boot overlay (`#boot`)** — BIOS-style lines typed out, themed to the topic
   (e.g. *spawning init process…* for OS, *titrating solution…* for chemistry),
   then the theme logo dissolves into the page. Click skips; a safety timeout ends it.
2. **Progress bar (`#progress`)** — thin reading-progress fill, amber→accent gradient.
3. **Side nav (`#nav`)** — auto-built from each `section.stage[data-name]`; dots show
   active/done; tooltips on hover; hidden under 900px.
4. **Hero (`#hero`)** — pulsing session chip (`LESSON n / total`), oversized title
   (one word stroked, one glowing), a sub-paragraph that opens with a hook tied to the
   **mission**, four meta cards (stages / sims / minutes / questions), a scroll prompt.
5. **Stages (`section.stage` × 6–10)** — one concept each:
   `.stage-tag` (e.g. `STAGE 03 · CONCEPT_KEY`) → `h2.stage-title` with one `<em>`
   highlighted word → `.lead` (key term in bold) → content (cards / sim / callouts) →
   usually a `.quiz` checkpoint. Wrap blocks in `.rv` (+ `.d1`–`.d4`) for staggered reveal.
6. **Final stage** — 3 integrative `.quiz[data-quiz][data-final]` questions, a scored
   `N/3` panel with range-based messages, confetti on perfect; optional `localStorage`
   persistence.
7. **Footer** — monospace credit line (source + course), link back to the hub.

## Component catalogue

All recipes are in the template's CSS — reuse the class, don't re-invent.

| Component | Class | Use it for |
|---|---|---|
| Concept card | `.card` in `.grid.c2/.c3/.c4` | 2–4 parallel ideas; hover-lift + glow |
| Flip card | `.flip` | vocabulary / "what's inside X"; 3-D flip on click or Enter |
| Callout | `.callout` (amber) / `.callout.cy` | exam point, intuition, **citations** |
| Term chip | `.term` / `.term.am` | every technical/foreign term in prose (ltr) |
| Sim shell | `.sim` → `.bar` + `.body` + `.status` + `.btn-row` | every simulation's chrome |
| Step pills | `.steps i` (`.on` / `.was`) | show progress through a sim's stages |
| Buttons | `.btn` / `.btn.am` / `.btn.ghost` | primary / "risky" / secondary actions |
| Quiz | `.quiz` (`[data-final]` for scored) | checkpoints + final |

When a stage needs a bespoke widget (a state-machine diagram, a Gantt chart, an
address translator), build it inside the `.sim` shell with the same tokens, the same
`.status` narration, and a working **Reset**. Save genuinely reusable widgets back to
the skill's `animations/` library per [ANIMATIONS-FORMAT.md](./ANIMATIONS-FORMAT.md).

## Designing a simulation (the heart of the format)

A sim is a **small state machine** the learner drives. Rules:

- **Controls:** a primary ▶ Run/Step button and a ↺ Reset. Reset must clear every
  pending `setTimeout`/`setInterval` (keep them in a `timers[]` array) and restore the
  start state — no half-finished animations bleeding into the next run.
- **Narrate, numbered, in the learner's language.** The `.status` line says what is
  happening *now* and *why*, step by step (① ② ③). The sim teaches through its
  narration as much as its motion.
- **Show state changing:** fill bars, moving tokens, flipping digits, a glow on the
  active element, a value that updates. The reader should *see* the mechanism.
- **Comparison beats assertion.** When two strategies differ, let the learner run both
  and compare a live number (e.g. "single program" vs "multiprogramming" CPU
  utilisation; FCFS vs SJF average wait). A side-by-side they trigger themselves is
  more convincing than any paragraph.
- **Easing signatures:** entrances `cubic-bezier(.2,.9,.3,1)`; pops/zaps
  `cubic-bezier(.2,1.6,.3,1)`. Use `.flash` for a hit, `.shake` for an error.

Sim ideas by shape: process/sequence → lane fill + step pills; state model → clickable
nodes (SVG) with an info panel; scheduling/allocation → coloured cells on a timeline;
mode/permission change → a token crossing a boundary with a flipping bit; race/ordering
→ two columns interleaving with a shared value going wrong.

## Quiz engine

- Checkpoint questions: `.quiz[data-quiz]`, correct option marked `data-ok="1"`. On
  click: lock, reveal the correct option, show verbal feedback, mini-confetti on right.
- **Distractors must be real misconceptions**, not nonsense — that's the teaching.
- Final quiz: add `data-final`; the engine counts globally and shows a scored panel
  with range-based messages and confetti on a perfect run.

## Writing tone

Second person, direct, with light domain humour (the OS lessons used *"the CPU never
gets bored"*, *"Kernel panic 😅"* — find the equivalent for your topic). Open each
stage with a question or promise, not a dry definition. Put exam-ready definitions in a
`📌` callout, phrased close to the source. Emoji belong in card/callout headers only,
never mid-paragraph.

## Pre-ship checklist

- [ ] User actually asked for the cool format (else use the default explainer).
- [ ] Boot sequence themed to the topic and skippable.
- [ ] `lang`/`dir` correct; RTL verified if applicable; terms in `.term` chips.
- [ ] Every source concept covered; claims cited; terminology matches `GLOSSARY.md`.
- [ ] ≥ 3 sims, each with a working Reset that clears all timers.
- [ ] Checkpoint after most stages + a scored 3-question final.
- [ ] Opens and runs from `file://` with no console errors; responsive to ~360px.
- [ ] Reskinned tokens/fonts/atmosphere — not left on the default unless it fits.
- [ ] Hub/index updated and linked, if the workspace keeps one.
- [ ] Reusable widgets saved back to `animations/` with an INDEX entry.
