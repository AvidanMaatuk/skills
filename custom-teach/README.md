# custom-teach

A stateful, animation-powered teaching skill for [Claude Code](https://claude.ai/code).

Based on the original [`teach`](https://github.com/mattpocock/teach) skill by [Matt Pocock](https://github.com/mattpocock). Extended with an animation library, curriculum coverage tracking, and interactive explainers.

## What it does

Teach any topic across multiple sessions in a single workspace directory. Each session picks up where the last left off, guided by:

- **MISSION.md** — why the user wants to learn this (grounds every session)
- **CURRICULUM.md** — what the mission requires, what's covered (with evidence), what's next
- **GLOSSARY.md** — compressed, reusable terminology
- **RESOURCES.md** — high-trust external sources
- **learning-records/** — ADR-style records of demonstrated understanding; used to calculate zone of proximal development

Explainers are saved as self-contained HTML files. They use animations tied directly to the concept being taught — not decoration — drawn from the bundled animation library.

## Install

Copy or symlink `custom-teach/` into `~/.claude/skills/` (name it `teach` or keep `custom-teach`).

```bash
cp -r custom-teach ~/.claude/skills/custom-teach
```

Then invoke it in Claude Code:

```
/teach What would you like to learn?
```

## Animation library

45 curated, self-contained HTML snippets in `animations/`, catalogued in `animations/INDEX.md` by pedagogical use (process, spatial, motion, state, emphasis, exercise, diagram, hook, reward).

The bundled assets (`assets/`) are copied into the workspace the first time an explainer is generated, so all HTML works offline.

## Additions over the original skill

| Feature | Original | custom-teach |
|---|---|---|
| Curriculum coverage map | — | CURRICULUM.md, evidence-gated |
| Animation library | — | 45 snippets + INDEX |
| Concept→technique mapping | — | anime.js / zdog / CSS / Lottie |
| Reuse ladder | — | search → modify → create → save |
| Decorative animation budget | — | ≤ 2 per explainer |
| Bundled offline assets | — | 5 libs, ~320 KB |

## Credits

| Project | Author | License |
|---|---|---|
| [teach](https://github.com/mattpocock/teach) (original skill) | [Matt Pocock](https://github.com/mattpocock) | MIT |
| [anime.js](https://animejs.com) | Julian Garnier | MIT |
| [Zdog](https://zzz.dog) | Dave DeSandro | MIT |
| [animate.css](https://animate.style) | Daniel Eden | MIT |
| [Magic CSS](https://www.minimamente.com/project/magic/) | Christian Pucci | MIT |
| [lottie-web](https://github.com/airbnb/lottie-web) | Airbnb | MIT |
| [front-end-daily-challenges](https://github.com/devSF/front-end-daily-challenges) | devSF | MIT |
