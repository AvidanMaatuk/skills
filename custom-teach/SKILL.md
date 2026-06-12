---
name: custom-teach
description: Teach the user a new skill or concept, within this workspace CUSTOM: add cariculam and animation.
disable-model-invocation: true
argument-hint: "What would you like to learn about?"
---

The user has asked you to teach them something. This is a stateful request - they intend to learn the topic over multiple sessions.

## Teaching Workspace

Treat the current directory as a teaching workspace. The state of their learning is captured in this directory in several files:

- `MISSION.md`: A document capturing the _reason_ the user is interested in the topic. This should be used to ground all teaching. Use the format in [MISSION-FORMAT.md](./MISSION-FORMAT.md).
- `CURRICULUM.md`: The coverage map for the topic - what the mission requires, what has been covered (with evidence), and what remains. Use the format in [CURRICULUM-FORMAT.md](./CURRICULUM-FORMAT.md).
- `GLOSSARY.md`: A glossary of terminology related to the topic. All workspace files should adhere to this terminology. Use the format in [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md).
- `RESOURCES.md`: A list of resources which can be explored to ground your teaching in contextual knowledge, or to acquire knowledge and wisdom. Use the format in [RESOURCES-FORMAT.md](./RESOURCES-FORMAT.md).
- `./learning-records/*.md`: A directory of learning records, which capture what the user has learned. These are loosely equivalent to architectural decision records in software development - they capture non-obvious lessons and key insights that may need to be revised later, or drive future sessions. These should be used to calculate the zone of proximal development. They are titled `0001-<dash-case-name>.md`, where the number increments each time. Use the format in [LEARNING-RECORD-FORMAT.md](./LEARNING-RECORD-FORMAT.md).
- `./assets/`: Local copies of the animation and styling libraries used by explainers (see Animation, below). Copied from the skill's own `assets/` directory the first time an explainer is generated.

## Philosophy

To learn at a deep level, the user needs three things:

- **Knowledge**, captured from high-quality, high-trust resources
- **Skills**, acquired through highly-relevant exercises devised by you, based on the knowledge
- **Wisdom**, which comes from interacting with other learners and practitioners

Before the `RESOURCES.md` is well-populated, your focus should be to find high-quality resources which will help the user acquire knowledge. Never trust your parametric knowledge.

Some topics may require more skills than knowledge. Learning more about theoretical physics might be more knowledge-based. For yoga, more skills-based.

## The Mission

Every teaching session should be tied into the mission - the reason that the user is interested in learning about the topic.

If the user is unclear about the mission, or the `MISSION.md` is not populated, your first job should be to question the user on why they want to learn this.

Failing to understand the mission will mean knowledge acquisition is not grounded in real-world goals. Exercises will feel too abstract. You will have no way of judging what the user should do next.

## The Curriculum

Once the mission is understood, derive `CURRICULUM.md` from it: the set of things the mission actually requires the user to learn, ordered by dependency. This is the coverage map - it answers "what should we do next?" and "how far along are we?" with evidence instead of guesswork.

- At the start of every session, read `CURRICULUM.md` alongside the learning records to choose the next item.
- An item is only marked covered when a learning record evidences demonstrated understanding - coverage is not exposure.
- The curriculum is living: add missing prerequisites as they surface, cut items that stop serving the mission, and record deliberate cuts under "Out of scope".

## Zone Of Proximal Development

The user should always feel as if they are being challenged 'just enough'. The scope of the topic being taught should feel extremely tight, should be directly tied into their mission.

The user may specify an exact thing they want to learn. If they don't, figure out their zone of proximal development by:

- Reading their `learning-records`
- Reading `CURRICULUM.md` to see what is covered and what the dependency order makes available next
- Teaching the most relevant available curriculum item that fits in their zone of proximal development

A user may tell you that they already know about that topic. If so, record it in their `learning-records` and mark the curriculum item covered.

## Glossary

A key part of acquiring knowledge is compressing knowledge into language. Once a term is known and understood, it can be used and combined in new ways to make more complex terms easier to understand.

Building the glossary should be done once you feel confident that the user understands the term. Glossaries should use a strict format, and use as concise a definition as possible.

## Acquiring Knowledge

Knowledge and skills usually need to be taught as a 1-2 punch. You teach the knowledge first, then get the user to practice the skills via exercises.

Knowledge should first be gathered from trusted resources, then taught to the user via HTML explainers. These explainers should be beautiful, adhere to the glossary, and be saved to the local file system where they can be reviewed later.

Explainers should be littered with citations - links to external resources to back up any claim made.

Explainers should be as interactive as possible, with "try this" callouts to let the user try the knowledge.

You should make opening the HTML explainer as easy as possible for the user, ideally with a CLI command they can run.

Once the user has read the knowledge, allow them to ask questions about it. Answer their questions directly, and amend the explainer if needed (or produce another one).

At this point, you can amend the glossary if it appears clear they understand a term.

## Animation

Animate the concept, not the page. An animation earns its place in an explainer when the concept itself involves motion, sequence, structure, or change - never as page decoration. The full workflow and snippet rules are in [ANIMATIONS-FORMAT.md](./ANIMATIONS-FORMAT.md); the library catalogue is [animations/INDEX.md](./animations/INDEX.md).

Map the concept to the technique:

- **Process / sequence / accumulation** → timeline animation. Use `gsap` (timelines, precise position control) for multi-step choreography; `anime.js` for lighter cases.
- **Scroll-driven / reveal-as-you-read / pin-and-explain** → `gsap` + `ScrollTrigger` (scrollytelling: ties the reveal to the reader's position).
- **Spatial structure / 3D / mechanical models** → `zdog`
- **Discrete state change** → CSS transitions; for **UI / interactive / component** concepts (toggles, accordions, dialogs, staggered card reveals) on a clean modern surface, use `shadcn` (`shadcn.css` tokens + tailwindcss-animate classes + the `data-state` pattern).
- **Emphasis on a key term or moment** → `animate.css` / `magic.css` classes, or a `gsap` stagger / springy ease, sparingly
- **Reward on exercise success, session hooks** → library `reward` / `hook` snippets, or a downloaded Lottie `.json` (playback only - never hand-author Lottie JSON)

When creating a `gsap` or `shadcn` animation, read the matching cheatsheet in [`references/`](./references/) first (`references/gsap.md`, `references/shadcn.md`) — it carries the correct API and do/don't list so the animation integrates correctly on the first pass. Always honour `prefers-reduced-motion`.

Hard budget: at most **2 decorative animations** (emphasis/reward) per explainer. Conceptual animations are limited only by whether each one teaches.

## Cool Explainer Format (opt-in)

There is a bolder, signature explainer style available: a single self-contained HTML lesson with a boot-up intro, neon blueprint surface, scroll-staged sections, hand-built interactive simulations, and a self-scoring quiz. The full spec and a working starter skeleton are in [COOL-EXPLAINER-FORMAT.md](./COOL-EXPLAINER-FORMAT.md) and [cool-explainer-template.html](./cool-explainer-template.html).

**Use it only when the user explicitly asks for it** — "make it cool", "the cool format", "cool explainer", "do it in the cool style", or similar. It is never the silent default; default explainers follow the guidance above. When the user does ask:

- Read [COOL-EXPLAINER-FORMAT.md](./COOL-EXPLAINER-FORMAT.md) and **follow it precisely** — start from `cool-explainer-template.html`, copy it into the workspace, reskin the `:root` tokens and fonts to the topic, and replace the stages.
- Keep the skill's pedagogy intact: mission-grounded, `GLOSSARY.md`-true, citation-backed, tied to the zone of proximal development. The cool format changes the *delivery*, not the teaching.
- Treat the choice as **sticky for the workspace**: once asked, later explainers in that topic keep the format. Note it in `CURRICULUM.md` so future sessions stay consistent.
- Run the format's pre-ship checklist before handing the explainer over.

For every animation, walk the reuse ladder defined in ANIMATIONS-FORMAT.md: search `animations/INDEX.md` first, reuse if a snippet fits, modify if one is close, create only when nothing exists - and **save anything created or meaningfully modified back to the skill's `animations/` directory with an INDEX.md entry**. The library compounds across topics; an unsaved animation is a wasted one.

### Asset wiring

The first time you generate an explainer in a workspace, copy the skill's `assets/` directory into the workspace (`./assets/`). Explainers reference these files by relative path (e.g. `<script src="./assets/anime.min.js">`), so the workspace stays self-contained, works offline, and can be shared. The bundled libraries: `anime.min.js`, `gsap.min.js`, `ScrollTrigger.min.js`, `zdog.dist.min.js`, `lottie_light.min.js`, `animate.min.css`, `magic.min.css`, `shadcn.css`. (Seeded `gsap`/`shadcn` snippets reference `../assets/...`; when embedding one into an explainer, rewrite the path to `./assets/...`.)

## Acquiring Skills

Skills should be taught through interactive exercises. There are several tools at your disposal:

- Interactive HTML explainers, using quizzes and light in-browser exercises - the `exercise` snippets in the animation library are good starting points for interactive widgets
- HTML explainers which guide the user through a list of real-world steps to take (for instance, yoga poses)
- In-agent quizzes, where you ask the user scenario-based questions about what they've learned

Each exercise should be based on a **feedback loop**, where the user receives feedback on their performance. This feedback loop should be as tight as possible, giving feedback immediately. Animation is a strong feedback channel: a correct answer can trigger a `reward` snippet; a wrong answer can animate _why_ it is wrong.

## Acquiring Wisdom

Wisdom comes from true real-world interaction - testing your skills outside the learning environment.

When the user asks a question that appears to require wisdom, your default posture should be to attempt to answer - but to ultimately delegate to a **community**.

A community is a place (online or offline) where the user can test their skills in the real world. This might be a forum, a subreddit, a real-world class (budget permitting) or a local interest group.

You should attempt to find high-reputation communities the user can join. If the user expresses a preference that they don't want to join a community, respect it.
