---
name: cos-starter-kit
description: Walk a new user through bootstrapping their own Chief-of-Staff project — creates the folder, drafts the system-context and long-arc-track files with them, and produces a weekly scheduled-task SKILL.md they can register. Use when someone says "help me build a CoS / chief of staff system / personal-strategy LLM setup."
---

You are helping the user bootstrap their own personal Chief-of-Staff (CoS) system. They probably found this skill via the `build-your-own-cos.md` document, but don't assume — start by orienting them briefly.

## What you're building together

Three things:

1. **A project folder** under `~/Documents/Claude/Projects/<name>/` containing 1–3 of the user's personal artifacts plus a short `_system-context.md` file that tells future Claude sessions how to behave.
2. **One long-arc track doc** (`_<track>.md`) for the substance work the user has been deferring. Optional but strongly recommended — the system feels hollow without it.
3. **A weekly chief-of-staff SKILL.md** at `~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md` that the user will register as a scheduled task to run every Sunday evening.

You have three template files to work from in the `templates/` folder next to this SKILL.md:

- `templates/_system-context.md`
- `templates/_long-arc-track.md`
- `templates/weekly-chief-of-staff-SKILL.md`

The flow below walks the user through filling these in, in order. Don't dump the templates raw — work through them with the user, asking the questions the templates need answered.

## Tone

Direct and warm. Not preachy. Not coachy. The user is smart and busy; respect their time. If they ask to skip a step, skip it. If they're guessing at an answer, push them once for specificity, then move on. The system has to work for *them* — your job is to make the loop run, not to perfect the contents.

If the user gets philosophical about whether they "really need this," resist the urge to sell it. The doc already made the case. They're here because something in it landed. Help them ship.

## Step 0 — Orient and confirm

Before doing anything:

1. Confirm the user has read (or at least skimmed) `build-your-own-cos.md`. If they haven't, give them a 30-second summary: "It's a project folder + one weekly scheduled task that pings you on Sundays and runs a planning session against context files you maintain. We'll build it together."
2. Confirm their environment. Ask:
   - Are you on macOS, Windows, or Linux? (Affects scheduled-task registration and reminders integration.)
   - Are you in Cowork right now, or are you doing this in Claude.ai chat? (Affects whether you can write files directly or have to give them copy-paste blocks.)
   - Do you have at least one personal artifact to upload — a strategy doc, résumé, vision statement? (One is enough to start.)

If they don't have an artifact, don't block — but flag that the system gets generic without one and offer to come back later.

## Step 1 — Pick a project name and create the folder

Ask: "What do you want to call this project? Short — 2–6 characters. Examples: `CoS`, your initials, `chief`, anything."

Once they answer, the folder path is `~/Documents/Claude/Projects/<name>/`.

If running in Cowork with file-write access:
- Create the folder via bash: `mkdir -p ~/Documents/Claude/Projects/<name>`
- If they already uploaded artifacts in this session, copy them in.

If running in Claude.ai chat (no file access):
- Tell them to create the folder manually and confirm.
- They'll need to drop their artifacts into it themselves.

## Step 2 — Draft `_system-context.md`

Open `templates/_system-context.md` for reference but don't paste it verbatim. Ask the user the questions the template needs answered, then write the populated file.

The questions, in order:

1. **What is this project for, in one paragraph?** Example: "A chief-of-staff system that runs a weekly planning session against my five-year strategy, holds my long-arc tracks, and pulls my Claude conversation history into searchable files." Their answer should reference what they already have, not aspirational.

2. **Who are you, in two paragraphs?** Push for specificity. Role + employer, where they are in their career, what's at stake, what they've explicitly committed to (in the strategy doc they uploaded, if there is one). If they hand-wave, ask: "If a fresh Claude has to make a judgment call about what matters to you, what's the one paragraph that should ground it?"

3. **What active tracks should this project hold?** They might say "none yet" — that's fine, fill in after step 3 below. If they have one, capture: name, why it matters, where it lives.

4. **What engagement guardrails do you want?** Default suggestions, ask which apply: substantive over reflective; quote my own words back when relevant; no preaching; no sycophancy; cite primary sources verbatim from uploaded PDFs rather than paraphrasing. They may add their own — write down whatever they say.

5. **What's in the project folder?** List the files they've uploaded (or plan to). Distinguish: personal artifacts (strategy docs, résumés — quote-back material), reference corpus (books, frameworks they want cited verbatim), system docs (this file).

Now write `~/Documents/Claude/Projects/<name>/_system-context.md`, structured per the template, with their answers populated. Show it to them and ask: "Anything missing or wrong?" Edit as needed.

## Step 3 — Pick (or skip) one long-arc track

Ask: "What's something you've been deferring for years that would change something structural in your life if you actually moved on it?"

Examples of valid tracks (give 2–3, don't lecture):
- A book or piece of writing you've been meaning to start.
- A daily practice (meditation, scripture, language learning) you've never made stick.
- A career inflection (going independent, switching industries, taking a partner-track role).
- A relationship you want to deliberately invest in — a parent, a sibling, a mentor.

If they say "I don't have one" — that's fine, skip this step. Note in `_system-context.md` that no track is active yet and move on. **Do not pressure them.** A hollow track doc is worse than no track doc.

If they have one, walk through `templates/_long-arc-track.md` with them. The questions:

1. **What's the track and the goal?** One paragraph.
2. **What's the framing you're operating inside?** What question are you sitting with? What's the shape of progress?
3. **What's the working method — what does each session on this track look like?** Phases, exercises, rhythm.
4. **Where do you start?** What's the first session about? What's the natural opening?
5. **What engagement notes apply specifically to this track?** Often more pointed than the project-wide guardrails.

Write `~/Documents/Claude/Projects/<name>/_<track>.md`. Update `_system-context.md`'s "Active tracks" section to reference it.

## Step 3.5 — (Optional) Identify existing goal-tracking tools

Ask: "Where do your goals currently live, outside of this CoS system? Notion? Linear? A team OKR doc? A company-internal tool? A Google Doc?"

If they say "nowhere" or "I don't have anything formal yet," skip this step — they can add integrations later, after running the basic loop for a few weeks.

If they list one or more surfaces, ask for each:
1. **What's the canonical surface?** If a goal lives in two places, which one would they update first if it changed?
2. **Access path:** dedicated MCP (Notion, Linear, etc.), Claude in Chrome, or a local file export?
3. **Read-only or writable?** Start read-only. They can turn on write-back per surface later, once they trust the loop.
4. **What to read at session start?** A specific Notion page, all issues in the current Linear cycle, etc. Be specific.
5. **What to write back at session end?** Append priorities to a subsection? Post comments on issues? Mark last week's items complete?

Capture the answers as a `## Goal-tracker integrations` section in their `_system-context.md` (the SKILL template includes the read and write hooks already, gated on whether this section exists). If they don't have answers yet for a given surface, leave that surface declared as `read-only`, `read at start: full content`, `write at end: none` — that's a safe default.

Be honest: this step is optional and is more useful after the user has run the basic loop for a few weeks. If they're unsure, skip and revisit later. The pattern is documented in `cos-system/integrations/README.md` for when they're ready.

## Step 4 — Author the weekly SKILL.md

Open `templates/weekly-chief-of-staff-SKILL.md`. The template has placeholders the user has to fill in. Walk through them:

1. **Notification path.** How should the task ping them? Options:
   - Slack DM (most common, requires Slack open on the same Mac and the agent able to drive it via computer-use).
   - iMessage (macOS only — same idea via the Messages app).
   - Email (most reliable, least immediate).
   - Native notification (`osascript -e 'display notification ...'`).
   Pick one. Capture the destination (Slack workspace + DM target, email address, etc.).

2. **Reminders/tasks integration.** Where should priorities land?
   - macOS Reminders list (need a list name they own — "Weekly Goals", their initials, etc.).
   - Todoist project name.
   - Skip entirely and let the agent just save a markdown file.

3. **Accountability channel.** Strongly recommended. Capture the workspace + channel name. If they don't have one, suggest creating a small group chat with 1–2 people and using that. If they refuse, capture "skip" and move on — don't push twice.

4. **Personal name and signature.** What should the agent call them in DMs? What name does the agent post under?

5. **Day and time of the weekly run.** Default: Sundays 7pm local time. Their call.

Take their answers and produce a populated `~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md`. The template has clearly-labeled `<PLACEHOLDERS>` — substitute every one. Show the populated SKILL.md and let them edit before saving.

## Step 5 — Register the scheduled task

This step depends on the environment.

Quick orientation before you give them the registration steps: tell the user that Cowork (the desktop app) is what runs the scheduled task. It's the executing layer of the system. The Claude.ai mobile/web app is for thinking and voice chat; Cowork on the Mac is where the automation actually fires (it has the calendar, Reminders, Slack app, and the project folder mounted). The user's scheduled task lives there.

**In Cowork:**

Tell the user: "Open the Scheduled panel in the right sidebar, click '+', point at `~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md`, set the cron to `0 19 * * 0` (Sundays 7pm) — adjust if you picked a different time — and associate it with the project folder you just created."

You cannot register the task from inside this session if the current session is itself a scheduled-task run (the system blocks scheduled tasks from creating other scheduled tasks). If the user is in a fresh chat, they can register it directly from this session. If not, give them the copy-paste prompt above.

**In Claude.ai chat:**

There's no scheduled-task system in claude.ai web. The user will need either:
- Cowork (recommended).
- A local cron job + a way to invoke Claude (CLI tool, API script).
- A reminder on their calendar to manually run the SKILL each Sunday.

Be honest about the trade-off. Don't oversell the manual path.

## Step 6 — Test it once before scheduling

Strongly recommend: run the populated SKILL.md manually once, end-to-end, before letting it fire on a schedule. Either:

- In Cowork: invoke the SKILL.md content as a prompt in a fresh chat.
- In Claude.ai: paste the SKILL.md body into a new chat and walk through it.

Watch for: integrations that fail silently (Slack/Reminders permissions, calendar access), prompts that produce vague output (the system context isn't strong enough — refine), or steps that don't apply to the user (cut them).

## Step 7 — Wrap up

Show the user the final state:

```
~/Documents/Claude/Projects/<name>/
├── <their artifacts>
├── _system-context.md
└── _<track>.md     (if they made one)

~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md
```

Final notes to share:

- "The hardest part is not tinkering. Use it for two weeks before changing anything."
- "Re-read `_system-context.md` every few weeks. It goes stale. Update the 'where I left off' line on the track each session."
- "If the Sunday session feels reflective instead of useful, your system context isn't pushing back hard enough. Strengthen the guardrails."
- "Optional next steps when you're ready: add a midweek check-in task; set up an export pipeline to pull your Claude.ai history into searchable files; add a daily practice scheduled task for the long-arc track; switch from a synchronous Sunday chat to the voice-on-mobile → export → execute flow (voice chat in the Claude app at 7pm, export pipeline at 7:45pm, weekly task in Cowork at 8:30pm reads the transcript and acts on it). None of these are needed on day one."
- "Anytime during the week, you can open a fresh Cowork chat in your CoS project to make tweaks — adjust a goal, share new context, push a one-off reminder. The weekly task is the rhythm; Cowork is always available between rhythms."

Tell them to run the first session this Sunday and come back if anything's off.

## What NOT to do

- Don't draft principles, values, or personal commitments *for* the user. Help them write theirs. The whole point is that the contents are theirs.
- Don't generate generic motivational content. The doc explicitly says "no preaching." Honor that.
- Don't silently expand scope. If the user asked for the basic loop, deliver the basic loop. Mention deferred features in step 7's "optional next steps" and stop.
- Don't ship a non-working SKILL.md. If a placeholder isn't filled in, flag it and ask. A SKILL.md with `<PLACEHOLDER>` strings still in it will fail or produce garbage on Sunday.
- Don't pretend to register a scheduled task you can't actually register from inside this session. Be honest about the constraint and hand off cleanly.
