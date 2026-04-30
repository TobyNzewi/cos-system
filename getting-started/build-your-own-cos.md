# Build your own Chief of Staff

_A small, durable system for running your own life with an LLM in the loop. Written for people who already use Claude and want something more deliberate than a chat history. Read time: ~10 minutes. Setup time: ~60 minutes._

---

## What this actually does

This sets up a weekly voice conversation with an AI chief of staff that walks you through reviewing your week, setting goals for the next one, and challenging whether what you're doing actually lines up with the principles you've said you care about. After the conversation ends, an automation reads the transcript and does the work — it updates your documents, pushes reminders to your phone, drops your priorities into a Slack channel like `#hyperbolicgoals` or whatever accountability surface you use, and saves a summary you can look back at next week.

---

## The weekly flow

Three stages, all stitched together so you only have to show up for the conversation:

1. **Sunday evening voice chat.** You open the Claude app on your phone — usually around 7pm, on a walk or sitting on the couch — and talk through your week. What got done, what didn't, what's coming up, where you're stuck. It's a real conversation, not a form.
2. **Export pipeline pulls the transcript.** A scheduled job grabs the conversation out of Claude.ai and drops it into local files where the rest of the system can read it. You don't do anything for this step.
3. **The weekly CoS task actions everything.** A second scheduled job reads the transcript and goes to work — creates calendar events for the commitments you made, pushes reminders to your phone, posts your priorities to Slack, updates your principles vault if anything shifted, saves a weekly summary. By the time you check your phone, the week is set up.

You can do this synchronously too — open Cowork on your laptop and chat with the agent directly — but the voice-on-phone-then-automation-on-laptop split is the pattern that holds up over months.

---

## Connecting your tools

The agent gets dramatically more useful when it can see your actual life instead of just what you tell it. You can wire it into Fireflies for meeting transcripts, Notion for goals and docs, your company's OKR system, Google Calendar, Slack, and basically anything else — through MCPs where they exist, or through Claude in Chrome where they don't.

The point isn't integration for its own sake. It's that the more your CoS knows about what you actually said you'd do this week — the meetings you took, the commitments you made out loud, the OKRs you're behind on — the better its pushback gets. A chief of staff who doesn't know your calendar can only ask generic questions. One who can see that you blocked off Thursday for deep work and then filled it with five back-to-back calls can ask the question that actually matters.

---

## The principles module

The system ships with a principles knowledge base — an Obsidian vault where you define what you actually believe across the categories that matter to you (career, personal growth, relationships, faith, health, financial, whatever else). The very first session walks you through discovering and writing those principles. Every session after that checks the goals you're setting against them and asks you to reflect on whether you've actually been living by them this week.

This is the part that turns it from a task tracker into something with teeth. Anyone can move tasks around a board. Almost no one sits down every week and asks themselves whether what they did this week is what they said they cared about.

---

## Who this is for

People who already use Claude and want something more deliberate than ad-hoc chats. This isn't a productivity app. It's a thinking partner that has memory, knows your calendar, and is set up to push back on you when you need it.

If you want a tool that quietly tracks tasks and never disagrees with you, this is the wrong thing. If you want something that will, every Sunday, ask you why you said you'd do the hard thing and then didn't — keep reading.

---

## The two layers

There's an operational layer and a substance layer. They're easy to confuse and the system fails when you do.

**Operational scaffolding** is the part that runs on a clock — the weekly check-in, the export pipeline that pulls your past Claude conversations into searchable files, any other automation. It's the "how do I get organized" layer.

**Substance** is what you're actually trying to do with your life — your North Star. This is the big directional thing you're working toward that's bigger than any weekly goal: a writing project, a fitness arc, a spiritual practice, a relationship you're rebuilding, a career inflection. The scaffolding exists to serve the substance. If your operational stuff is humming and the substance work isn't moving, the system is failing at its actual job. Build the operational layer, but design every part of it to push you toward the substance.

---

## The two surfaces — Claude app vs. Cowork

Once the system has been running for a few weeks you'll notice you're using two different surfaces for two different things. Naming them helps:

**Claude app (mobile or web) = thinking and planning.** Voice chat in your CoS project from anywhere, no setup, no Mac required. Useful in the car, on a walk, between meetings. But it has no access to your calendar, Reminders, Slack app, or filesystem — it can only talk.

**Cowork (desktop app) = executing.** Cowork has the foreground Mac apps (Calendar, Reminders, Slack), MCPs (Google Calendar, Gmail), and your project folder mounted. This is where files get written, reminders get pushed, Slack posts get sent. Also where your scheduled tasks actually run.

The pattern that emerges: think on the phone, execute on the desktop. The weekly Sunday flow codifies this — voice chat in the Claude app at 7pm to plan, then export pipeline at 7:45pm transports the transcript into local files, then the weekly CoS task in Cowork at 8:30pm reads the transcript and acts on it.

Outside the Sunday flow, you can open a fresh Cowork chat in your CoS project anytime to make tweaks: adjust a goal, share a piece of context, ask it to update a doc, push a one-off reminder. If a conversation in the Claude app needs to be actioned immediately rather than waiting for the next Sunday's export, the path is: copy/paste the conversation (or share the `claude.ai/share/...` link) into a Cowork chat from your phone and ask it to do the work.

You don't have to use both surfaces. The minimum viable system is just Cowork with a weekly scheduled task — the voice-chat layer is an enhancement. But once you have it, the split is real and worth naming.

---

## Connecting your existing goal-tracking tools (optional)

Most of us already have a place where goals live — a Notion personal dashboard, a team OKR system, a Google Doc strategy doc, a Linear cycle, a company-internal tool. The fastest way to make CoS feel grounded — instead of feeling like a parallel siloed tracker — is to point it at those existing surfaces.

Two lifecycle hooks make this work:

1. **Read at session start.** Before the agent proposes priorities, it pulls the current state of your goal surfaces into context. The priorities it sets are aware of your company OKRs, ongoing initiatives, and whatever else lives in those tools.
2. **Write back at session end.** After priorities are committed, the agent updates the goal surface with this week's priorities — appending to a Notion page, posting comments on Linear issues, marking last week's items complete.

The point: your goal surface stays the source of truth. CoS reads from it and writes to it; CoS doesn't replace it. Cowork lets you connect MCPs (Notion, Linear, Asana, etc.) or drive web apps via Claude in Chrome, so you can wire CoS to whatever tools your work and life already use. The integration is bespoke per user — there's a generic pattern, but the specifics are yours to configure.

**To wire it up:**
1. List your goal surfaces. Pick the canonical one for each goal.
2. For each, decide the access path: a dedicated MCP if available, Claude in Chrome if not, or a local file if that's enough.
3. Decide read-only or writable per surface — start read-only, add write-back to surfaces you trust the loop on.
4. Declare the integrations in your `_system-context.md` under a `## Goal-tracker integrations` section.
5. The weekly SKILL has read and write hooks already wired up; they activate automatically when integrations are declared.

The full pattern, conventions, and example shapes (Notion, Linear, Google Doc) are documented in `cos-system/integrations/README.md`. This is a Phase 2 enhancement — get the basic loop working for two weeks first, then layer this in once you know what your weekly task actually needs to read and write.

---

## What you'll need

- A laptop you keep on most of the day (the scheduled tasks run locally).
- Claude desktop with Cowork mode. The Claude.ai web/mobile app is a useful complement for voice-chat planning but isn't where the automation runs.
- ~60 minutes for the first pass. Less if you already have a strategy doc to upload.
- 1–3 personal artifacts you're willing to put in a project folder. A résumé, a goals doc, a five-year plan — whatever names what you actually care about. **This is the most important input.** Without it, the system can only be generic.
- Optional but strongly recommended: an accountability partner you'll DM weekly summaries to, or a small group chat. Posting your goals to yourself in private is not the same as posting them to people.

You do not need to be technical. The starter-kit skill walks you through this. If you're comfortable creating folders and editing markdown files, you have enough.

---

## The shape of the system (architecture)

```
~/Documents/Claude/Projects/<your-cos>/
├── <your strategy doc>                 ← personal artifacts you upload
├── <your résumé / LinkedIn>            ← whatever grounds "who I am"
├── <reference corpus, if any>          ← books, frameworks you anchor on
├── _system-context.md                  ← the spine. Read first by every session.
├── _north-star.md                      ← your North Star (optional but recommended)
└── _summary-<corpus>.md                ← distilled summaries of any large PDFs

~/Documents/Claude/Scheduled/
├── weekly-chief-of-staff/SKILL.md      ← the planning session
└── <export-pipeline>/SKILL.md          ← optional: pulls your Claude history (advanced)
```

Three files do almost all the work:

1. **`_system-context.md`** — a single page that tells any new Claude session what's been built, how to behave, and where to look for what. Without this, every chat starts from zero.
2. **A North Star doc** (`_north-star.md`) — captures the substance work so it survives across sessions. Not required, but the system feels hollow without it.
3. **The weekly SKILL.md** — a numbered script the scheduled task runs. Tells Claude what to do when it fires on Sunday: read the context files, ping you on Slack/iMessage, run a planning session, save a summary, push priorities to your reminders app.

Everything else — the exports pipeline, additional scheduled tasks, the corpus PDFs — is optional polish.

---

## How to set it up

Two paths. Pick one.

### Path A: run the starter-kit skill (recommended)

The companion `cos-starter-kit` skill walks you through every step interactively. Install it, invoke it inside Cowork (or paste it into a Claude.ai chat), and answer the questions it asks. It creates the folder, drafts your system-context file with you, helps you pick your North Star, and produces a working weekly SKILL.md you can register as a scheduled task. ~30–45 minutes start to finish.

### Path B: do it manually

If you'd rather build piece by piece:

1. **Create the project folder.** `~/Documents/Claude/Projects/<name>/`. Pick a short name (`CoS`, `cos`, `chief`, your initials).
2. **Drop in your personal artifacts.** Whatever names what you care about — strategy doc, résumé, a vision statement, the last performance review you wrote about yourself. One to three files is enough.
3. **Write `_system-context.md`** using the template in the starter kit. It's short — under a page. Cover: what this project is, who you are in two paragraphs, what your North Star is, what guardrails apply (preachy? no. sycophantic? no.).
4. **Pick your North Star.** Something you've been deferring for years. Write `_north-star.md` using the template — it captures the goal, the framework, where you left off, and engagement notes. Don't pick three; pick one.
5. **Author the weekly SKILL.md.** Copy the template, change the name in the kickoff message, the Slack/iMessage destination, the reminders list name, the channel name. Test it once by running it manually before scheduling.
6. **Register it as a scheduled task.** In Cowork: right-sidebar → Scheduled → "+", point at the SKILL.md, set a cron (Sundays 7pm is a good default), and associate it with your project so it inherits the context folder.
7. **Wait until Sunday.** Don't tinker further until you've run the loop once.

---

## What goes in the templates (the spine)

Three template files live in the starter kit. Here's what each one is for and the minimum viable version of each.

### `_system-context.md` — minimum viable

```
# <Project name> — system context

_Last updated: <date>. Read this before doing anything substantive in this project._

## What this is

One paragraph: what this project is for and who it serves.

## Who I am — synthesis for a fresh Claude

Two paragraphs. Name, role, what you're working on, what's at stake, what
you've explicitly committed to (cite the strategy doc).

## North Star

Name, doc filename, one-sentence summary, why it matters, where it lives
operationally.

## Scheduled tasks

For each: what it does, when it runs, where its SKILL.md lives.

## Engagement guardrails

How you want Claude to behave. Examples: substantive over reflective, quote my
own words back when relevant, no preaching, no sycophancy. Yours will differ.

## Files in this folder

What's here and how to use it. Distinguish "primary source — read verbatim"
from "summary — load every session" from "personal artifact — quote back."
```

### `_north-star.md` — your North Star

```
# <North Star name>

_Last updated: <date>. Read this before engaging on <topic>._

## What this North Star is

One paragraph: the goal and why now.

## The framing

The intellectual frame you're operating inside. Where you started, what
question you're sitting with, what you've decided is the shape of progress.

## The working method

How sessions on this North Star run. Phases, exercises, what each session
produces.

## Where I left off

What was true at the end of the last session. The next session reads this
to know where to pick up. Update it every session.

## Engagement notes — what's been working

The shape of useful conversation on this North Star. Specific.
```

### Weekly SKILL.md — minimum viable

```
---
name: weekly-chief-of-staff
description: Weekly planning session. Reviews last week, sets priorities, pushes to reminders, posts to accountability channel.
---

You are acting as [YOUR NAME]'s chief of staff. This runs every [DAY] at [TIME].

## First: ping me

Send a DM to me on [Slack/iMessage/email] saying the session is ready.
Wait for me to reply before continuing.

## Required reading before starting

Read these in full. They are the source of truth.

1. ~/Documents/Claude/Projects/<your-cos>/_system-context.md
2. ~/Documents/Claude/Projects/<your-cos>/_north-star.md  (if you have one)

## Session steps

1. Calendar review — pull the upcoming week. Flag overload and gaps.
2. Last-week review — read ~/Documents/Claude/cos-weekly-summary.md and
   walk through what got done, partially done, dropped.
3. North Star check — explicitly ask whether your North Star moved this week.
   This is the easiest thing to skip and the most important not to.
4. Set priorities — top 3–5 for the week. Push back if I'm overcommitting.
   Tag each with the day(s) it's most relevant.
5. Conflicts and risks — call them out.
6. Save summary to ~/Documents/Claude/cos-weekly-summary.md.
7. Push priorities to [Reminders/Todoist/etc.] as dated items.
8. Post to [accountability channel] in the format the channel uses.
9. Send me a DM with the top 3.

## Tone

Direct, supportive, efficient. Chief of staff, not therapist.
```

---

## Engagement guardrails (so the system doesn't become noise)

The fastest way to make this useless is to let it become reflective. The model is happy to mirror you for hours; you don't need that.

**Tell it explicitly to push back.** In your `_system-context.md`, write the sentence "push back when I'm overcommitting; quote my own words back to me when I'm avoiding something I've already named." This kind of instruction actually works.

**Cite primary sources.** If you upload books or frameworks, the model should pull verbatim from the PDF, not paraphrase from training data. Say so.

**No sycophancy.** Most people notice it within ~3 messages. Banning it in the system context cleans things up immediately.

**Preserve continuity in writing, not in chat history.** Every session should leave behind an updated file (the North Star doc, the weekly summary). Chat history isn't memory; the files are.

**One North Star at a time.** Three becomes none.

---

## What breaks (failure modes)

Things will break. The system is designed to fail loudly so you can fix it.

**Scheduled task fires while your laptop is closed.** It just doesn't run. Either keep the laptop open at the scheduled time or move the cron to a window when it usually is.

**The weekly task drifts into vagueness.** This happens when `_system-context.md` gets stale. Re-read it every few weeks; update the "North Star" and "where I left off" sections. The doc is a living thing.

**The North Star stalls.** Most common failure. Usually means you picked the wrong one, or you set it up too elaborately. Simplify. The minimum viable North Star is one paragraph of "what I'm working on" updated weekly.

**You start tinkering instead of using.** A real risk for technical people. Set a rule: no changes to the system between Sunday sessions. Use it as it is for two weeks before iterating.

**The model gives you a tidy summary instead of friction.** Tell it again, more explicitly, to disagree when it disagrees. If it still won't, your system context isn't strong enough.

---

## What to skip on the first pass

Don't build these on day one. They're worth doing eventually.

- An export pipeline that pulls your full Claude.ai history into searchable files. Useful, but only after you have weekly summaries piling up. Set up the weekly task first; come back to this in a month.
- The voice-chat-on-mobile-then-Cowork-executes flow. This is the mature pattern (Stage 1 voice chat in the Claude app at 7pm → Stage 2 export pipeline at 7:45pm → Stage 3 weekly CoS in Cowork at 8:30pm reads the transcript and acts on it). Worth doing once the basics work, but on day one the synchronous "open Cowork at 7pm and chat with the agent" pattern is fine. The voice/Cowork split adds value when you start wanting to plan from your phone or somewhere away from the Mac.
- Multiple scheduled tasks (mid-week check-ins, daily morning practices). Start with one. Add more only when the first is reliably useful.
- Custom MCP servers, plugins, complex integrations. The friction of building them is real and they don't matter until the basic loop is humming.
- A polished public version of your system. Use it privately for a quarter first. Most of what you'll learn comes from running it, not designing it.

---

## A note on what makes this work

The thing that surprised me about running this for a few months: the most valuable artifact isn't the weekly summaries or the priorities or the Slack posts. It's the North Star doc. Because it forces you to write down where you left off — every session, in your own words — it becomes the only place that holds the through-line of work that doesn't fit on a quarterly horizon.

Almost everyone has at least one of those threads. The one you've been deferring for three years. The one that would change something structural if you actually moved on it.

Pick that one.

---

## Files in the starter kit

The companion `cos-starter-kit` ships with:

- `SKILL.md` — the setup scaffolder. Invoke this in Cowork or paste into Claude.ai to walk through setup.
- `templates/_system-context.md` — fill-in-the-blank system context.
- `templates/_north-star.md` — fill-in-the-blank North Star doc.
- `templates/weekly-chief-of-staff-SKILL.md` — fill-in-the-blank weekly task.
- `templates/README-for-folder.md` — a one-page orientation you can drop into your project folder so future-you remembers the setup.

---

_If you build a version of this and it works for you, tell me what you changed. The shape gets sharper with more reps._
