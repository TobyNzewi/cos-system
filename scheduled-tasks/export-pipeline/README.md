# Export pipeline

The export pipeline is an optional, advanced component of the CoS system. It pulls your full Claude.ai conversation history into searchable local markdown files so your scheduled tasks (and ad-hoc sessions) can reference what you've discussed across all your Claude conversations.

**Don't build this on day one.** Get the weekly task running first. Come back to this after a month, once you have weekly summaries piling up and want the system to be able to reference your broader conversation history.

## What it does

1. **Triggers a Claude.ai data export** — navigates to `claude.ai/settings/data-privacy-controls` via the Chrome MCP and clicks "Export data."
2. **Waits for the export email** — polls Gmail for the "Your data is ready for download" email from Anthropic.
3. **Downloads the ZIP** — fetches the export ZIP via in-tab JavaScript (same-origin fetch using your authenticated claude.ai session).
4. **Recovers project linkage** — the export ZIP doesn't preserve which conversations belong to which claude.ai project. The pipeline hits the live API (`GET /api/organizations/{org}/chat_conversations`) to recover the `project_uuid` per conversation and builds a mapping file.
5. **Parses to markdown** — a Python parser converts the ZIP into per-conversation markdown files, organized by project.

## Output structure

```
parsed/
├── index.md                                    ← all conversations, newest first
├── projects.md                                 ← project metadata + counts
├── conversations/{date}-{slug}-{uuid8}.md      ← one file per unlinked conversation
├── projects/{slug}/{date}-{slug}-{uuid8}.md    ← conversations grouped by project
├── projects/{slug}/README.md                   ← per-project index
├── project-docs/{slug}/{filename}              ← knowledge docs from projects
└── meta/manifest.json                          ← run metadata
```

## How it fits in the Sunday flow

In the mature three-stage Sunday pattern:

- **7:00 PM** — You have a voice chat in the Claude app (the thinking stage).
- **7:45 PM** — The export pipeline runs (this task), pulling your conversation history including the 7pm voice chat into local markdown.
- **8:30 PM** — The weekly chief-of-staff task runs, reads the freshly-parsed voice chat transcript, and acts on it.

The export pipeline is stage 2 — it bridges the thinking surface (Claude app) and the executing surface (Cowork). Without it, the weekly task can still run, but it won't have access to what you discussed in the voice chat. You'd need to either paste the conversation into Cowork manually or run the planning session synchronously.

## Prerequisites

- **Chrome MCP** (`Claude in Chrome`) connected and authenticated to claude.ai
- **Gmail MCP** connected (for polling for the export email)
- **Python 3** available in the Cowork sandbox
- **An authenticated claude.ai session** in Chrome (the pipeline uses your browser cookies for the API calls)

## Key technical details

- **Export rate limit:** roughly once per 24 hours. If you trigger manually close to the scheduled run, the second trigger will hit a cooldown.
- **Download URL is single-use.** The link in the email works exactly once. The pipeline fetches via JavaScript (not by navigating to it) to avoid accidentally consuming the link.
- **Project linkage is fragile.** The live API endpoint that provides `project_uuid` per conversation is undocumented and could change. The parser falls back gracefully to a flat layout if the mapping is missing.

## Building your own

The export pipeline involves account-specific details (org ID, Chrome session, Gmail access) that make it hard to ship as a generic template. If you want to build one:

1. Find your org ID: it's in the URL when you're on claude.ai (the UUID in the path).
2. Write a SKILL.md that follows the five steps above, substituting your org ID.
3. The parser scripts (Python) are generic — the account-specific parts are the trigger and download steps.

This is the most technically complex part of the CoS system and the most likely to break when Anthropic changes their UI or API. Treat it as a nice-to-have, not a requirement.
