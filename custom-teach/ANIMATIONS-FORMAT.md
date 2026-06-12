# Animation Library Format

The animation library lives in the skill's own `animations/` directory (next to this file, **not** in the teaching workspace). It is a compounding asset: it grows across every topic and every workspace you teach in. Its catalogue is [animations/INDEX.md](./animations/INDEX.md).

## The reuse ladder

Whenever an explainer needs an animation, walk this ladder and stop at the first rung that works:

1. **Reuse** — search `animations/INDEX.md` by pedagogical use and description. If a snippet fits, embed it (adapted to the explainer's palette and labels as needed).
2. **Modify** — if a snippet is close but not right, copy it, adapt it, and save the adaptation back as a new snippet *when the change is reusable* (e.g. "orbit model" → "electron shell model"). Cosmetic recolouring does not warrant a new entry.
3. **Create** — build a new snippet from scratch. Pick the library by what the concept needs, not by habit:
   - **CSS** transitions/keyframes — simple state flips and emphasis (lightest; default for one-shot motion).
   - **shadcn** (`shadcn.css`) — UI / interaction / discrete-state concepts on a clean modern surface (cards, buttons, accordions, dialogs, staggered reveals). Uses the tailwindcss-animate enter/exit classes and the `data-state` pattern. See [references/shadcn.md](./references/shadcn.md).
   - **GSAP** (`gsap.min.js`, `+ ScrollTrigger.min.js`) — sequencing (timelines), scroll-linked reveal, staggers, runtime control (pause/reverse/seek/scrub), or springy/elastic easing. See [references/gsap.md](./references/gsap.md). Prefer GSAP over `anime.js` when you need scroll-linking, playback control, or precise multi-step choreography.
   - **anime.js** — lightweight JS timelines/staggering/SVG when GSAP would be overkill.
   - **zdog** — 3D structure and mechanical models.
   - **lottie** — only for playing back a downloaded `.json`.

   When creating a **GSAP** or **shadcn** snippet, read its reference file in [`references/`](./references/) first — it carries the correct API and the do/don't list so the animation is right the first time.

Every created or meaningfully modified animation **must** be saved to `animations/` and added to `INDEX.md`. An unsaved animation is a wasted one.

## Snippet rules

- One snippet = one self-contained `.html` file, openable directly in a browser.
- No CDN links, no references to files outside the skill — inline all CSS/JS, base64-inline any image. (A snippet may assume the bundled `assets/` libraries only when embedded into a workspace explainer; the standalone file in `animations/` should inline what it needs to run alone.)
- Keep the demonstrated *concept* front and centre; strip decorative chrome when adapting a snippet for teaching.
- **Heavy bundled libraries (`gsap.min.js`, `ScrollTrigger.min.js`, `shadcn.css`) are not inlined** — they are too large to paste into every file. A GSAP/shadcn snippet references them by relative path to the sibling assets dir (`../assets/gsap.min.js`, `../assets/shadcn.css`), which resolves both when the file is opened standalone from `animations/` and after the asset is copied into a workspace. This is offline and dependency-free (no CDN); it is the one allowed reference outside `animations/`. When the snippet is embedded into a workspace explainer, rewrite the path to `./assets/...`.
- Lottie snippets are the other exception to single-file: store the downloaded `.json` next to the snippet, named identically (`my-animation.html` + `my-animation.json`).

## Naming

`<topic-or-concept>-<what-it-shows>.html`, dash-case, e.g. `tcp-handshake-sequence.html`, `binary-tree-insertion.html`. The seeded snippets keep their original numbered names; new snippets do not take numbers.

## INDEX.md entry

Append one row to the table in `animations/INDEX.md`:

```md
| <file> | <use> | <library> | <one-line description: what it shows, what concept it teaches> |
```

- `use` is one of: `process`, `spatial`, `motion`, `state`, `emphasis`, `exercise`, `diagram`, `hook`, `reward` (defined at the top of INDEX.md).
- `library` is one of: `css`, `js`, `anime`, `gsap`, `shadcn`, `zdog`, `lottie`.
- The description is what future sessions search against — write it for retrieval, naming both the visual ("ball hopping up stairs") and the teachable concept ("discrete incremental progress").
