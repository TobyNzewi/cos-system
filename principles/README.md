# Principles module

A separate Obsidian vault for the principles you're trying to live by — articulated in your own words, tested against scripture or experience, refined weekly.

This module is **optional but high-leverage**. Most CoS users will benefit from it after a few weeks of running the basic weekly loop, once the question "why did I pick *those* priorities and not others?" starts surfacing. That's the question the principles vault answers, and the question the weekly CoS task can then test priorities against.

## Why a separate vault

Principles are not weekly priorities, not project notes, not journal entries. They're a stable substrate that everything else gets tested against. Mixing them in with daily working files makes them feel like another thing to maintain. Putting them in their own vault — and naming it bluntly — keeps them load-bearing.

Inspired by Ray Dalio's *Principles*: write your principles down in your own words, test them against reality, refine them over time. The CoS-specific extension: also test them against the people, frameworks, or scripture you're already drawing on. Pure self-construction is a yellow flag.

## What's in this directory

```
principles/
├── README.md              ← this file
├── vault-template/        ← a complete, generic vault you can copy to ~/Documents/Principles/
└── examples/              ← three generic example principle notes for shape
```

The `vault-template/` directory is the drop-in. Copy it to `~/Documents/Principles/`, open the folder in Obsidian, and the vault is ready to populate.

## How to set it up

1. **Copy the vault template** to your home directory:
   ```bash
   cp -R cos-system/principles/vault-template ~/Documents/Principles
   ```

2. **Open `~/Documents/Principles/` in Obsidian.** The `.obsidian/` directory in the template tells Obsidian to recognize the folder as a vault. (Obsidian is free; download from obsidian.md if you don't have it.)

3. **Run the principles-discovery session.** This is a one-time voice walkthrough that articulates your initial 12–18 principles. The session lives in your CoS project (`~/Documents/Claude/Projects/<your-cos>/principles-discovery/SKILL.md`) — see the `getting-started/` directory of this repo for the bootstrap. If you don't have that yet, you can do it manually by walking through each `categories/*.md` file's prompts and writing principle notes by hand.

4. **Wire the weekly CoS task to read it.** Two new segments get added to your weekly SKILL.md (see `cos-system/scheduled-tasks/weekly-chief-of-staff/SKILL.md` for the canonical version):
   - **Principles Alignment Check** after priorities are set: compares this week's goals to the principles, flags misalignment.
   - **Weekly Principles Reflection** at the end: captures what was lived, what was hard, any changes, and saves a dated reflection note.

5. **Run for a few weeks before tinkering.** Principles get sharper through the weekly reflection — not through editing the discovery output. Resist the urge to refactor in the first month.

## Vault structure

```
Principles/
├── _index.md              ← master index of all principles, grouped by category
├── _about.md              ← vault explainer and conventions
├── categories/            ← one note per category, with prompts + wiki links to principles in that category
├── principles/            ← one note per principle, with template-frontmatter and structured sections
├── reflections/           ← one note per weekly reflection, dated YYYY-MM-DD
└── .obsidian/             ← Obsidian config (auto-managed once you open the vault)
```

Six categories, by convention:
- **Career & Professional** — work posture, peers, effort, advancement
- **Personal Growth** — development, learning, change, pain handling
- **Relationships** — family, partnership, friendship, mentorship
- **Faith & Spirituality** — beliefs, practice, the trust-vs-ego fork
- **Health & Wellness** — body, sleep, exercise, mental health
- **Financial** — money posture, risk, generosity, lifestyle

You can rename or merge categories if these don't fit. The discovery skill assumes six but is structurally agnostic — substitute in your `_index.md` and the category notes.

## Per-note conventions

- **Wiki links for cross-references.** Obsidian double-bracket syntax: `[[principles/be-the-first-to-name-the-hard-thing]]`. Renames propagate; the graph view becomes useful.
- **Filenames are kebab-case slugs.** "Be the first to name the hard thing" → `be-the-first-to-name-the-hard-thing.md`.
- **Principles are stated in the first person, declarative.** Not "should be honest" — "I name what's broken before someone else does."
- **Retired principles move to `principles/_retired/`** rather than getting deleted. The history of what you tried to believe is itself useful.
- **Reflections are append-only.** Don't edit past reflections — they're a record of where you were when.

## What goes in `principles/` vs. `categories/`

- A `principles/<name>.md` file is the canonical home of a principle: statement, why it matters, source, examples, tensions, related, reflections. See `vault-template/principles/_template.md`.
- A `categories/<category>.md` file is an index — a list of wiki links to principles in that category, plus a one-paragraph framing of what the category is about, plus prompts the discovery session uses. Don't put principle content in category files.

## Example principles

See `examples/` for three generic example principle notes — one each from career, personal-growth, and financial. They're meant to show the *shape* of a good principle note, not to be copied into your vault. Your principles will be different and should sound like you, not like the examples.

## Troubleshooting

**"Obsidian doesn't see my vault."** Make sure the `.obsidian/` directory copied over (it's hidden — `cp -R` should include it but some shells skip dotfiles by default). Re-copy or create an empty `.obsidian/` directory inside the Principles folder and restart Obsidian.

**"My principles all sound generic."** This is the most common failure mode. Two fixes: (1) push for a concrete example for every principle — if you can't name a recent decision the principle applied to, the principle is aspirational, not real; (2) test each principle against the question "would I disagree with someone for whom this isn't a principle?" If the answer is no, the principle is too universal to be useful.

**"I have 30 principles and the weekly reflection is unwieldy."** You probably collected a list of values rather than principles. Principles are *operative* — they shape decisions. Values are *stated*. Move the non-operative entries to `principles/_retired/_values-not-principles.md` or just delete them. Aim for 12–18 active principles total.

**"My goals never align with my principles."** Either your principles are aspirational (you wrote down who you want to be, not how you actually decide) or your goals are downstream of pressure rather than principle (your week is set by deadlines, not values). The weekly alignment check is meant to surface this — sit with the tension before "fixing" either side.

## Repo cross-references

- `cos-system/scheduled-tasks/weekly-chief-of-staff/SKILL.md` — the weekly task that reads from this vault (alignment check + reflection).
- `cos-system/getting-started/build-your-own-cos.md` — the parent doc that introduces the CoS system. The principles module is mentioned there as Phase 2 work.
- `cos-system/getting-started/cos-starter-kit/` — the bootstrap skill. A future version will offer to scaffold this principles module alongside the basic CoS setup.
