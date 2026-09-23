# Claude Code tune-up

A kit for cleaning up your Claude Code setup. It gives you one command, `/tune-up`, that has Claude review your `CLAUDE.md` files and skills, tell you in plain words what it would change, back everything up, and make the changes you approve.

## Why bother

Your `CLAUDE.md` and skills were probably written with help from older Claude models. Those models needed a lot of hand-holding: step-by-step recipes, rules in ALL CAPS, the same instruction repeated in three places. Current models don't need that, and it can make them worse: more cautious, more questions, more rigid. It also costs usage, because `CLAUDE.md` and every skill's description are sent with every message.

Setups also go stale. Notes like "we used to do X, now we do Y", finished plans, and paths that moved all confuse Claude a little each time.

A tune-up keeps what matters (your facts, preferences, and real rules) and removes the rest.

## Install (once)

In Claude Code, type:

```
/plugin marketplace add tysszl/claude-tuneup
/plugin install tune-up@tyler-tune-up
```

Then restart Claude Code.

## Use

Open Claude Code in a project folder and type:

```
/tune-up
```

You can also say what you want:

- `/tune-up my global setup` — your personal `CLAUDE.md`, skills, and settings used in every project
- `/tune-up the invoice skill` — one skill

Claude will inventory the setup, check it against the real project, and give you a short list of proposed changes. Nothing changes until you say yes. Before editing, it saves a backup (a Git commit, or a copy in `~/.claude/tune-up-backups/`) and tells you how to undo. Afterward, start a new session so the changes load.

Run it on each project once, then again every few months or after a new model comes out.

Use Claude Opus 5.5 for this (`/model opus`); the judgment calls are the point.

## Settings that save usage

The tune-up will offer these, but you can set them yourself. Open `~/.claude/settings.json` (or ask Claude to) and add:

```json
{
  "env": {
    "CLAUDE_CODE_AUTO_COMPACT_WINDOW": "400000"
  }
}
```

This makes Claude summarize a long conversation at 400,000 tokens instead of waiting until nearly 1 million. Every message resends the whole conversation, so a huge conversation gets expensive fast, and Claude works better with less clutter anyway.

## Habits that save usage

- **One task per session.** When you switch to something unrelated, type `/clear`. Long sessions make every message cost more.
- **Don't switch models or turn plugins on and off mid-session.** Claude Code reuses the unchanged part of the conversation at a discount, for about an hour. Switching models or tools throws that discount away.
- **Back after more than an hour?** The discount has expired. If the session was long, ask Claude for a short summary of where things stand, type `/clear`, and paste the summary in.
- **Raise effort only when needed.** `/effort high` for a hard problem; the default is fine for most work.
- **Look before guessing.** `/context` shows what's filling Claude's memory, `/usage` shows how much you're using, and `/skill-doctor` shows which skills you never use.
