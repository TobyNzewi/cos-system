# <PROJECT NAME> — system context

_Last updated: <YYYY-MM-DD>. Read this file in full before doing anything substantive in this project. It is the source of truth for who I am, what's in motion, and how I want you to behave._

## What this is

<ONE PARAGRAPH. What this project is for. What it serves. Concrete — reference what you actually have, not what you wish you had.>

Two layers worth distinguishing:

- **Operational scaffolding** — the scheduled tasks (weekly chief-of-staff, etc.) and the artifacts they produce. The "how do I get organized" layer.
- **Substance** — my North Star and the track that serves it, captured in `_<track>.md`. The direction I want my life's work heading. The scaffolding exists to serve this. If the operational stuff is humming and the substance work isn't moving, the system is failing at its actual job.

The project lives at `~/Documents/Claude/Projects/<NAME>/`.

## Who I am — synthesis for a fresh Claude

<TWO PARAGRAPHS. Name. Role + employer. Where you are in your career or life arc. What you've explicitly committed to in your strategy doc (cite it). What's at stake right now. What patterns of yours are worth knowing.>

<If you have a multi-year strategy doc — name it, say what it is, treat it as the authoritative artifact. Tell future Claude to quote it back to you when relevant.>

## North Star

### <Track name>

**Doc:** `~/Documents/Claude/Projects/<NAME>/_<track>.md` — read this in full before engaging me on <topic>.

**Summary:** <ONE PARAGRAPH. My North Star and what this track is working toward.>

**Why it matters:** <What this represents. The weekly task should explicitly check on this each week.>

<If you have additional tracks over time, add them as secondary tracks. Keep this section focused on one primary North Star direction.>

## Scheduled tasks

### 1. weekly-chief-of-staff

**When:** <day> at <time> local (cron `<expr>`).
**SKILL.md:** `~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md`
**What it does:** <ONE PARAGRAPH. Notification path, planning flow, where summaries land, where priorities go (reminders/todoist), accountability post if any.>

<Add additional scheduled tasks as you build them. Keep this list current.>

## Engagement guardrails

How I want you to behave when working with me on this project. Honor these by default.

- **<Guardrail 1>.** <Why it matters in your own words.>
- **<Guardrail 2>.**
- **<Guardrail 3>.**

Suggested defaults if you're unsure what to write:

- **Substantive over reflective.** I do not want generic listening. Pushback, conviction-building, and friction.
- **Quote my own words back when relevant.** If I've already named a pattern in my strategy doc, surface it instead of paraphrasing.
- **Concrete over vague.** Cite primary sources verbatim from uploaded PDFs. Don't paraphrase from training data.
- **No preaching.** Don't lecture. Don't moralize.
- **No sycophancy.** I notice it.

## Files in this folder

The files here are deliberate, not incidental. Each one earns its place by being something a session needs.

**Personal artifacts (source of truth for who I am and what I'm committed to):**

- `<filename>` — <one line. What it is. When to use it. "Quote it back to me when X."> 

**Reference corpus (canonical works I'm anchoring on — uploaded so you can cite passages and frameworks accurately rather than paraphrasing from training data):**

- `<filename>` — <one line. What it is. "Don't recall from memory; pull verbatim from this PDF.">

**Distilled summaries (loaded into context every session — saves token budget vs. loading the full PDFs):**

- `<filename>` — <one line. What it covers and how to use it (navigation aid → pull verbatim from the PDF when accuracy matters).>

**System docs (the "how this works" layer):**

- `_<track>.md` — North Star track doc. Read before engaging on <topic>.
- `_system-context.md` — this file. Read first by every new session in this project.

## Known soft spots / what could break

<List the failure modes you've noticed. Things like: "the export pipeline assumes my Chrome is logged in," "the Slack flow depends on a specific app being foregrounded," "the reminders integration uses a list name I own." Better to write them once than rediscover them when something breaks at 7pm Sunday.>

## Open improvements (deferred)

<Things you've decided not to build yet and why. Keep this list small — it's a parking lot, not a roadmap.>
