# second-brain template

A second brain: an [Obsidian](https://obsidian.md) vault of plain markdown that an AI agent (Claude) keeps up to date. You tell it things ("remember the boiler was serviced today, next one due next October") and it files them onto the right page. Obsidian shows you a dashboard of what's due, renewals, birthdays and projects.

- `CLAUDE.md` holds every rule the agent follows. `AGENTS.md` is a symlink to it.
- `Home.md` is the dashboard. `wiki/` is what the agent maintains, starting from `wiki/index.md`.
- `Weekly/` is your to-do list, one note per week. `Notes/` is your own writing, which the agent never rewrites.
- New notes land in `Inbox/`, and a GitHub Action files them within minutes.

## Setup (about an hour, best done together)

### 1. Make your copy

1. On GitHub: **Use this template > Create a new repository**. Make it **Private**. Call it `second-brain`.
2. Clone it to the computer: `git clone https://github.com/<you>/second-brain.git ~/second-brain`. On Windows, use GitHub Desktop.

### 2. Obsidian on the computer

1. Install [Obsidian](https://obsidian.md) and **Open folder as vault** on the clone.
2. When asked, **Trust author and enable plugins**. That turns on the bundled **Git** plugin (obsidian-git), which commits and syncs every 10 minutes and pulls on startup. If it asks for GitHub credentials, sign in with GitHub Desktop or `gh auth login` first.
3. Open `Home.md` and pin it.

### 3. Claude

1. A Claude subscription (Pro or above).
2. Install [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (`npm install -g @anthropic-ai/claude-code` or the native installer), or use the Claude desktop app's Code tab, pointed at the vault folder.
3. In the vault folder run `claude` and say: **"set up my second brain"**. It sees that `wiki/Me.md` is still a template and runs the setup interview: you, your people, work, home, cars, money (names only), health, interests. It writes pages as you go and commits them.

### 4. Automation (GitHub Actions)

1. In the vault folder run `claude setup-token`, then sign in. It prints a long-lived token.
2. On GitHub: repo **Settings > Secrets and variables > Actions > New repository secret**, name `CLAUDE_CODE_OAUTH_TOKEN`, value the token.
3. **Actions** tab: enable workflows, then run **file inbox** and **weekly lint** once by hand (**Run workflow**) to check they work.

You now have:
- **file inbox**: files `Inbox/` on every push that touches it, and daily at about 23:10.
- **weekly lint**: Sunday evening. Makes next week's to-do note (with carried-over to-dos, renewals and birthdays coming up), tidies pages, scans for secrets.

### 5. Phone (optional)

Pick one:
- **Obsidian Sync** (paid, simplest): turn it on in Obsidian on the computer and the phone. The computer's Git plugin pushes everything to GitHub, including captures made on the phone.
- **Git on the phone**: Obsidian mobile with the same Git plugin and a GitHub token. Free, slower, and sometimes needs a manual pull.

On the phone, any new note goes to `Inbox/` and gets filed.

### 6. Time zone

The default is `Europe/London`. To change it, edit **Settings** in `CLAUDE.md` and `TZ` in both files in `.github/workflows/`, and adjust their `cron` times (cron runs in UTC).

## Day to day

- **Remember something**: tell Claude "remember that ...", or make a new note in Obsidian.
- **To-dos**: this week's note in `Weekly/`.
- **What's coming up**: `Home.md`.
- **Ask anything**: "when's the car MOT?", "what did Sarah want for her birthday?". Claude answers from the vault and names the page.
- **Change how it works**: tell Claude ("stop tracking X", "put recipes in their own folder"). It updates `CLAUDE.md` so every future session follows the change.

## Never put in the vault

Passwords, PINs, account, card, sort code, policy or passport numbers, 2FA or recovery codes. Keep those in a password manager. The agent refuses to write them and removes any it finds.

## Credits

Obsidian skills in `.claude/skills/` are from [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) (MIT, see `LICENSE-obsidian-skills`). Git sync by [obsidian-git](https://github.com/Vinzent03/obsidian-git) (MIT).
