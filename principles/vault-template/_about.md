# About this vault

A separate Obsidian vault for the principles I'm trying to live by. Not part of any other vault, not under my CoS project — its own thing, on purpose.

## Why a separate vault

Principles are upstream of weekly priorities. Mixing them with working files makes them feel like another thing to maintain; isolating them keeps them load-bearing.

Inspired by Ray Dalio's *Principles*: write your principles down in your own words, test them against reality, refine them over time. The extension I'm running: principles also get tested against external anchors — scripture, frameworks, mentors — not just my own experience. Pure self-construction is a yellow flag.

## How it works with the CoS system

The weekly chief-of-staff task at `~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md` reads from this vault every Sunday in two places:

1. **Principles Alignment Check** (after the goals are set): the agent reads each principle and compares it against this week's goals. Goals get labeled `aligned`, `neutral`, or `misaligned` — and misaligned ones get challenged in the summary, not papered over.
2. **Weekly Principles Reflection** (at the end of the session): the agent captures what was lived, what was hard, what to add/update/retire, and saves a dated reflection note in `reflections/`.

Outside the Sunday flow, the principles vault is also read by:
- The `principles-discovery` SKILL — a one-time voice walkthrough that populates the initial 12–18 principles.
- Any ad-hoc Cowork chat where I want to reason about a decision against my principles.

## Vault structure

```
Principles/
├── _index.md              ← master index (this vault's homepage)
├── _about.md              ← this file
├── categories/            ← one note per category, with prompts + wiki links to principles
├── principles/            ← one note per principle, populated from the discovery session
└── reflections/           ← one note per weekly reflection, dated
```

## Conventions

- **Wiki links for cross-references.** Obsidian double-bracket syntax: `[[principles/<name>]]`.
- **Filenames are kebab-case slugs of principle names.**
- **Principles are stated in the first person, declarative form.** "I name what's broken in a project before someone else does" — not "should be honest."
- **Keep the vault empty until the discovery session runs.** Manual seeding defeats the point.
- **Retired principles move to `principles/_retired/`** rather than being deleted.
- **Reflections are append-only.** Past reflections are a record of where you were when.

## What this vault is NOT

- Not a personal-growth journal. Reflections are tight (lived/hard/changes/score). Not free-form.
- Not a goals tracker. Goals live in CoS. Principles are upstream of goals.
- Not a quotes collection. Anchor passages go under `Source/Inspiration` in the principle note.
