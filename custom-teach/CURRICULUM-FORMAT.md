# Curriculum Format

`CURRICULUM.md` lives in the teaching workspace. It is the coverage map for the topic: what the mission requires the user to learn, what has been covered, and what remains. It is how you choose what to teach next instead of guessing.

## Lifecycle

1. **Derive** — once `MISSION.md` is populated, derive an initial curriculum from the mission and from trusted resources in `RESOURCES.md`. Scope it to the mission: a curriculum for "build a home lab" is not the syllabus of a networking degree.
2. **Consult** — at the start of every session, read the curriculum together with the learning records to pick the next item inside the zone of proximal development.
3. **Update** — when learning records demonstrate understanding, move items to covered (link the record). When teaching reveals missing prerequisites or the mission shifts, add/remove/reorder items. The curriculum is a living document, not a contract.

## Template

```md
# Curriculum: {Topic}

Derived from [[MISSION.md]] on {date}. Revised: {date}.

## Covered

- [x] {Item} — [[learning-records/0001-slug.md]]

## In progress

- [ ] {Item} — {what remains before it counts as covered}

## Remaining

- [ ] {Item} — {one line: why the mission needs this}
- [ ] {Item} — {…}

## Out of scope

- {Item} — {why it was cut; stops re-litigating}
```

## Rules

- An item counts as **covered** only when a learning record evidences it — coverage is demonstrated understanding, not material presented. Every covered item links its record.
- Keep items mission-sized: each should be teachable in one to three sessions. Split items that balloon.
- Order the **Remaining** list by dependency, not by importance — prerequisites first.
- **Out of scope** is as valuable as the rest: it records deliberate cuts so future sessions don't drift back into them.
- If more than ~20% of remaining items stop serving the mission, re-derive the curriculum rather than patching it, and note the revision date.
