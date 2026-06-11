# Animation Library Format

The animation library lives in the skill's own `animations/` directory (next to this file, **not** in the teaching workspace). It is a compounding asset: it grows across every topic and every workspace you teach in. Its catalogue is [animations/INDEX.md](./animations/INDEX.md).

## The reuse ladder

Whenever an explainer needs an animation, walk this ladder and stop at the first rung that works:

1. **Reuse** — search `animations/INDEX.md` by pedagogical use and description. If a snippet fits, embed it (adapted to the explainer's palette and labels as needed).
2. **Modify** — if a snippet is close but not right, copy it, adapt it, and save the adaptation back as a new snippet *when the change is reusable* (e.g. "orbit model" → "electron shell model"). Cosmetic recolouring does not warrant a new entry.
3. **Create** — build a new snippet from scratch. Prefer, in order: CSS transitions/keyframes for simple state and emphasis; `anime.js` for timelines, staggering and SVG; `zdog` for 3D structure; `lottie` only for playing back a downloaded `.json`.

Every created or meaningfully modified animation **must** be saved to `animations/` and added to `INDEX.md`. An unsaved animation is a wasted one.

## Snippet rules

- One snippet = one self-contained `.html` file, openable directly in a browser.
- No CDN links, no references to files outside `animations/` — inline all CSS/JS, base64-inline any image. (A snippet may assume the bundled `assets/` libraries only when embedded into a workspace explainer; the standalone file in `animations/` should inline what it needs to run alone.)
- Keep the demonstrated *concept* front and centre; strip decorative chrome when adapting a snippet for teaching.
- Lottie snippets are the one exception to single-file: store the downloaded `.json` next to the snippet, named identically (`my-animation.html` + `my-animation.json`).

## Naming

`<topic-or-concept>-<what-it-shows>.html`, dash-case, e.g. `tcp-handshake-sequence.html`, `binary-tree-insertion.html`. The seeded snippets keep their original numbered names; new snippets do not take numbers.

## INDEX.md entry

Append one row to the table in `animations/INDEX.md`:

```md
| <file> | <use> | <library> | <one-line description: what it shows, what concept it teaches> |
```

- `use` is one of: `process`, `spatial`, `motion`, `state`, `emphasis`, `exercise`, `diagram`, `hook`, `reward` (defined at the top of INDEX.md).
- `library` is one of: `css`, `js`, `anime`, `zdog`, `lottie`.
- The description is what future sessions search against — write it for retrieval, naming both the visual ("ball hopping up stairs") and the teachable concept ("discrete incremental progress").
