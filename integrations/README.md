# Goal-tracker integrations

A pattern for pointing CoS at the goal-setting tools you already use — Notion, Linear, Asana, a Google Doc, your company OKR system, whatever. So the weekly task has real context on what you're working toward, and so it can update those surfaces when goals are set or completed.

This is intentionally a *pattern*, not a turnkey integration. Cowork lets you connect MCPs and run computer-use against any app — the configuration that's right for *your* tools is yours to write. This module gives you the shape; you fill in the specifics.

## The core idea

Most people already have somewhere their goals live. A Notion personal dashboard. A team OKR doc. A company-internal tool. The fastest way to make a CoS's weekly planning feel grounded — instead of feeling like a parallel tracker — is to have it read from that surface at the start of the session and write back to it at the end.

Two lifecycle hooks:

1. **Read at the start.** Before the agent proposes priorities, it pulls the current state of your existing goal surfaces into context. This means the priorities it proposes are aware of company OKRs, quarterly objectives, ongoing initiatives, and whatever else lives in those tools.

2. **Write at the end.** After priorities are set and the weekly summary is saved, the agent updates the goal surface with this week's priorities — adding them to the relevant Notion page, ticking completed items off a Linear cycle, appending to a Google Doc. The goal surface stays the source of truth; CoS just keeps it in sync.

## How to wire it up

**Step 1 — enumerate your goal surfaces.** Sit down and list every place a goal of yours currently lives. Common ones:

- Notion (personal dashboard, team workspace)
- Linear / Jira / Asana (company task or OKR system)
- Google Docs / Microsoft Word (annual review docs, strategy docs)
- A company-internal tool (Workday OKRs, Lattice, etc.)
- Slack canvases or pinned messages
- A whiteboard photo, a piece of paper, a notes app

If a goal lives in more than one place, pick the canonical one — the one you'd update first if a goal changed. The others can be downstream.

**Step 2 — pick the access path for each.** For each surface, there are three options ranked from best to worst:

1. **A dedicated MCP.** If a Notion MCP, Linear MCP, Asana MCP, etc. is connected to your Cowork session, that's the best path — fast, structured, no UI brittleness. Check the MCP registry for what's available.
2. **Claude in Chrome.** If there's no MCP for your tool but it has a web UI, the Chrome extension can navigate it, read content, and update fields. Slower and more brittle than an MCP but works for almost anything.
3. **A local file.** If your goals live in a Google Doc you've also exported as `.docx` to your CoS folder, or a Markdown file you maintain, the agent can just read the file. Lowest fidelity but highest reliability — no auth, no UI changes.

For each surface, also note: is this *read-only* (for context) or *writable* (the agent can update it)? Write access usually requires more thought — if the agent updates a Notion page incorrectly, that has real consequences. Start read-only; add write back to surfaces you trust the loop on.

**Step 3 — declare your integrations in your `_system-context.md`.** Add a section like:

```markdown
## Goal-tracker integrations

The weekly CoS task reads from these surfaces at the start of the session and writes to them at the end. Each is configured with a name, access path, what to read, and what (if anything) to write.

### Personal goals — Notion (`personal-okrs` page)
- **Access:** Notion MCP
- **Page ID:** `<id>` (or page title slug)
- **Read at start:** the "Q2 2026 personal goals" section.
- **Write at end:** append this week's priorities under the "Weekly check-ins" subsection with the date.

### Company OKRs — Linear (current cycle)
- **Access:** Linear MCP
- **Read at start:** issues assigned to me in the current cycle.
- **Write at end:** none (read-only — leadership owns this surface).

### Annual strategy — Google Doc
- **Access:** local export at `~/Documents/Claude/Projects/<cos>/strategy-2026.docx` (refreshed manually monthly).
- **Read at start:** full doc as context.
- **Write at end:** none (read-only).
```

The structure here is the contract between your `_system-context.md` and the weekly SKILL. The SKILL reads this section to know what to do.

**Step 4 — add the two hooks to your `weekly-chief-of-staff/SKILL.md`.** The canonical version of the SKILL in this repo (`cos-system/scheduled-tasks/weekly-chief-of-staff/SKILL.md`) already includes both hooks, gated on whether your `_system-context.md` declares any integrations. Either copy that version, or add to your existing SKILL the two steps shown there.

## Conventions

- **Read-only is the default.** Adding write access to a surface is a deliberate decision — it means the agent can actually change something visible to other people (your manager, your team). Start read-only; turn on write back per surface as you build confidence.
- **One direction at a time.** The agent reads at the start, executes the planning, writes at the end. It does not read mid-session and write mid-session — that creates loops and version-skew.
- **Idempotent writes.** Writes should be append-or-update, not overwrite. If the same week is run twice (manual + scheduled), the surface should end up in the same state, not with duplicates.
- **Failure is loud.** If a Notion API call fails or a Chrome navigation breaks, the agent surfaces the failure in the weekly summary and DMs the user — it doesn't silently skip and pretend success.
- **The goal surface is the source of truth.** CoS reads from it and writes to it; CoS doesn't replace it. If a goal changes, change it in the goal surface, not in CoS — CoS will pick it up next Sunday.

## Two example shapes

These are illustrative — the specifics depend on your tools.

### Notion personal-OKRs page

You maintain a Notion page titled "2026 personal OKRs" with a "Weekly priorities" subsection where each week appends a dated bullet list.

- **Read at start:** Notion MCP fetches the page; the agent extracts the active OKRs from the "Q2 2026 OKRs" subsection.
- **Write at end:** Notion MCP appends to the "Weekly priorities" subsection: a new bullet with the week's Monday date and this week's top 3 priorities as sub-bullets.

The OKRs aren't touched (read-only); the weekly priorities subsection grows over time (append-only).

### Linear team cycle

You're on a team where work is tracked in Linear cycles, and your weekly priorities should map to existing Linear issues.

- **Read at start:** Linear MCP fetches issues in the current cycle assigned to you, plus any issues you've manually starred.
- **Write at end:** for each priority that maps to a Linear issue, the agent posts a comment on that issue: "CoS week-of-{date}: this is on my plate this week." For priorities without a Linear issue, the agent flags them in the weekly summary so you can decide whether to create issues.

This shape keeps Linear as the work surface; CoS is just doing the planning around it.

### Google Doc strategy doc

You have a "Annual strategy" Google Doc that you refresh quarterly. It's read-only context for the weekly task.

- **Read at start:** the agent reads a `.docx` export of the doc that you keep in your CoS project folder. You re-export it manually whenever you update the strategy.
- **Write at end:** none.

This is the lowest-effort integration — no MCP needed, no auth, just a stale-but-good-enough export.

## Repo cross-references

- `cos-system/scheduled-tasks/weekly-chief-of-staff/SKILL.md` — the canonical weekly task with both integration hooks already wired up, gated on the `_system-context.md` declarations.
- `cos-system/getting-started/build-your-own-cos.md` — the parent doc; the integrations module is mentioned there as a Phase 2 enhancement.
- `cos-system/getting-started/cos-starter-kit/SKILL.md` — the bootstrap. A step in there asks new users about their existing goal surfaces and helps them declare integrations during setup.
