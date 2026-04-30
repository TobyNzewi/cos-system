# cos-starter-kit

A small kit for bootstrapping your own Chief-of-Staff project — a personal-strategy LLM setup that runs a weekly planning session, holds your long-arc tracks, and shares context across all your sessions.

For the philosophy and architecture, read `build-your-own-cos.md` (one folder up). This README just describes what's in the kit.

## What's in the kit

```
cos-starter-kit/
├── README.md                                  this file
├── SKILL.md                                   the setup scaffolder — invoke this
└── templates/
    ├── _system-context.md                     project spine, fill-in-the-blank
    ├── _long-arc-track.md                     one long-arc track, fill-in-the-blank
    ├── weekly-chief-of-staff-SKILL.md         the weekly scheduled task, fill-in-the-blank
    └── README-for-folder.md                   drop-in folder readme
```

## How to use it

**In Cowork:** Drop the `cos-starter-kit/` folder into your Cowork plugins or skills location, then ask Claude to invoke `cos-starter-kit`. It walks through the setup interactively.

**In Claude.ai chat:** Paste the contents of `SKILL.md` into a new chat as the first message. Claude will then walk you through the setup. You'll need to create the folders and files yourself — Claude will give you the contents to paste.

**Reading first:** If you'd rather understand the system before kicking off the scaffolder, read `build-your-own-cos.md` end to end. ~10 minutes.

## What you'll have at the end

```
~/Documents/Claude/Projects/<your-name>/
├── <your personal artifacts>
├── _system-context.md
└── _<track>.md           (if you opted in to a long-arc track)

~/Documents/Claude/Scheduled/weekly-chief-of-staff/SKILL.md
```

A scheduled task registered to run weekly, plus a project folder Claude reads as context whenever you start a session inside it.

## Time budget

- ~10 minutes reading.
- ~30–45 minutes running the scaffolder.
- ~5 minutes registering the scheduled task.
- One full Sunday session before deciding if it works for you.

## License / attribution

MIT. Lift, fork, modify. If you build a version of this and it works for you, open an issue and say what you changed.
