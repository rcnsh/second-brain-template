---
type: tech
status: active
updated: 2026-10-30
source: agent
tags: [tech, second-brain]
---
# Second Brain

This vault: an Obsidian vault of plain markdown, kept in a private GitHub repo. Rules for agents are in `CLAUDE.md` at the root (`AGENTS.md` is a symlink to it).

## How to use it

- Open `Home.md` for the dashboard: due soon, renewals, projects, birthdays.
- To-dos go in this week's note in `Weekly/`.
- To capture anything, make a new note. New notes land in `Inbox/` and are filed onto the right pages automatically.
- Ask any agent "remember that ..." and it records the fact.

## How sync works

- Repo: (filled in at setup)
- Devices with the vault: (filled in at setup)
- The Obsidian Git plugin commits and syncs edits every 10 minutes and pulls on startup.
- GitHub Actions file `Inbox/` on every push that touches it and daily at 23:10, and run the weekly lint on Sundays. Both need the repo secret `CLAUDE_CODE_OAUTH_TOKEN`.

## Where secrets live

- Password manager: (filled in at setup)
