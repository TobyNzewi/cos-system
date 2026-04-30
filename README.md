# CoS — Chief of Staff AI System

A personal chief-of-staff system built on Claude. It runs a weekly planning loop, holds long-arc personal development tracks across sessions, and executes against your calendar, reminders, and accountability channels — so your goals don't just sit in a doc.

## What this is

CoS is a project folder on your computer. It contains a few files about you (a strategy doc, a résumé, whatever names what you care about), a short "system context" file that tells future Claude sessions what's already been built and how to behave, and one or two scheduled tasks that run on a clock and message you when they fire. The scheduled tasks read the project's context every time they run, so they share a memory you maintain in writing. That's the whole system.

## Why it exists

Most people have a strategy doc or a goals list somewhere. It sits in a folder. Nothing in the week pulls on it. What's missing is a thin, persistent layer between that long-arc strategy and the actual week — something that:

- Knows who you are and what you're working on, without re-explaining every chat
- Shows up on its own each Sunday and runs a planning session against last week's goals
- Has continuous memory across conversations via files, not chat history
- Holds at least one long-arc track — a thread of work that takes years, not days

Off-the-shelf productivity tools track tasks; they don't think with you. CoS is an LLM with persistent context, a calendar, and a clock.

## Architecture

### The two layers

**Operational scaffolding** — the weekly check-in, the export pipeline, any other automation. The "how do I get organized" layer.

**Substance** — what you're actually trying to do with your life. A writing project, a fitness arc, a spiritual practice, a career inflection, a relationship you're rebuilding. The scaffolding exists to serve the substance. If your operational stuff is humming and the substance work isn't moving, the system is failing at its actual job.

### The two surfaces

**Claude app (mobile or web) = thinking and planning.** Voice chat from anywhere. No setup, no Mac required. Useful in the car, on a walk, between meetings. But no access to your calendar, reminders, or filesystem — it can only talk.

**Cowork (desktop app) = executing.** Has access to your Mac's foreground apps (Calendar, Reminders, Slack), MCPs (Google Calendar, Gmail), and your project folder mounted. This is where files get written, reminders get pushed, posts get sent. Also where your scheduled tasks actually run.

The pattern that emerges: **think on the phone, execute on the desktop.**

### The Sunday flow (mature pattern)

Three stages, ~90 minutes total:

```
7:00 PM — Voice CoS chat (you, in the Claude app)
           Think out loud. Review last week. Surface priorities.
           Output: a conversation transcript.

7:45 PM — Export pipeline (scheduled task, Cowork)
           Pulls your Claude conversation history into local markdown files.
           The voice chat from 7pm is included.

8:30 PM — Weekly chief-of-staff (scheduled task, Cowork)
           Reads the voice chat transcript and ACTS on it.
           Sets priorities, flags conflicts, writes the weekly summary,
           pushes priorities to Reminders, posts to your accountability channel.
```

You don't need to start with the full three-stage flow. The minimum viable system is just the weekly scheduled task running in Cowork. Add the voice-chat and export layers later.

## What's in this repo

```
cos-system/
├── README.md                          ← you are here
├── getting-started/
│   ├── build-your-own-cos.md          ← the full guide (~10 min read)
│   └── cos-starter-kit/
│       ├── README.md
│       ├── SKILL.md                   ← interactive setup scaffolder
│       └── templates/
│           ├── _system-context.md     ← project spine, fill-in-the-blank
│           ├── _long-arc-track.md     ← long-arc track, fill-in-the-blank
│           ├── weekly-chief-of-staff-SKILL.md
│           └── README-for-folder.md
├── scheduled-tasks/
│   ├── weekly-chief-of-staff/SKILL.md ← the weekly planning task
│   ├── midweek-checkin/SKILL.md       ← mid-week nudge
│   └── export-pipeline/README.md      ← how the export pipeline works
├── principles/                        ← optional module: Obsidian vault for principles
│   ├── README.md                      ← module explainer + setup
│   ├── vault-template/                ← drop-in Obsidian vault (categories, templates)
│   └── examples/                      ← 3 example principle notes for shape
├── integrations/                      ← optional module: connect existing goal apps
│   └── README.md                      ← read-at-start + write-back pattern (Notion, Linear, etc.)
├── templates/
│   └── weekly-summary-template.md     ← template for the weekly summary file
└── examples/
    └── long-arc-track-example.md      ← example of a filled-in track doc
```

The `principles/` and `integrations/` modules are optional Phase 2 enhancements. Get the basic weekly loop running first, then layer them in.

## Getting started

### Quick start (~60 minutes)

1. **Read** [`getting-started/build-your-own-cos.md`](getting-started/build-your-own-cos.md) — the full guide. ~10 minutes.
2. **Run the starter kit.** Copy `getting-started/cos-starter-kit/` to your machine. In Cowork, invoke the `SKILL.md` — it walks you through setup interactively. Or paste its contents into a Claude.ai chat and follow the prompts. ~30–45 minutes.
3. **Register the scheduled task.** In Cowork: right sidebar → Scheduled → "+" → point at the generated `weekly-chief-of-staff/SKILL.md` → set a cron (Sundays 7pm). ~5 minutes.
4. **Wait until Sunday.** Don't tinker. Run it once end-to-end before changing anything.

### What you'll need

- A Mac you keep open most of the day (scheduled tasks run locally)
- Claude desktop with Cowork mode
- 1–3 personal artifacts: a strategy doc, résumé, goals doc — whatever names what you care about
- Optional: an accountability partner or group chat to post weekly goals to

### What you'll have at the end

```
~/Documents/Claude/Projects/<your-project>/
├── <your personal artifacts>
├── _system-context.md             ← the spine — read first by every session
└── _<track>.md                    ← your long-arc track (if you opted in)

~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md
```

A scheduled task that fires every Sunday, reads your context, reviews your week, sets priorities, pushes them to your reminders app, and posts to your accountability channel. Plus a project folder that gives every Claude session shared memory.

## What to skip on the first pass

- The export pipeline (pulling your full Claude.ai conversation history). Set up the weekly task first; come back to this in a month.
- The voice-chat → export → execute three-stage flow. Start with synchronous Sunday chats in Cowork. Add voice later.
- Multiple scheduled tasks. Start with one.
- Custom MCP servers, plugins, complex integrations.

## What breaks (and what to do)

**Scheduled task fires while your laptop is closed.** It just doesn't run. Keep the laptop open at the scheduled time, or move the cron.

**The weekly task drifts into vagueness.** Your `_system-context.md` got stale. Re-read it every few weeks; update the "active tracks" and "where I left off" sections.

**The long-arc track stalls.** Most common failure. Usually means you picked the wrong track or set it up too elaborately. Simplify.

**You start tinkering instead of using.** Set a rule: no changes between Sunday sessions. Use it for two weeks before iterating.

**The model gives you tidy summaries instead of friction.** Your system context isn't pushing back hard enough. Strengthen the engagement guardrails.

## Staying updated

This is a living repo, not a one-time download. I'm actively running this system myself and pushing updates as I learn what works, what breaks, and what to add. The templates, SKILL files, and guidance will evolve as the underlying tools (Cowork, scheduled tasks, MCPs) mature and as I accumulate more reps.

If you cloned this to build your own CoS, you can pull updates anytime:

```bash
cd cos-system
git pull origin main
```

Your personal files (`_system-context.md`, `_<track>.md`, your artifacts) live in your own project folder, not in this repo — so pulling updates won't overwrite your stuff. What you'll get are improved templates, new scheduled-task patterns, and lessons learned from running the system over time.

If you're part of the group chat and something breaks or you find a better pattern, say so — the framework gets sharper with more people running it.

## License

MIT. Lift, fork, modify. If you build a version of this and it works for you, open an issue and say what you changed.
