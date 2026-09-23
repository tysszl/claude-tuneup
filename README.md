# Claude Code tune-up

A kit for cleaning up your Claude Code setup. It gives you one command, `/tune-up`, that has Claude review your `CLAUDE.md` files and skills, tell you in plain words what it would change, back everything up, and make the changes you approve.

## Why bother

Your `CLAUDE.md` and skills were probably written with help from older Claude models. Those models needed a lot of hand-holding: step-by-step recipes, rules in ALL CAPS, the same instruction repeated in three places. Current models don't need that, and it can make them worse: more cautious, more questions, more rigid. It also costs usage, because `CLAUDE.md` and every skill's description are sent with every message.

Setups also go stale. Notes like "we used to do X, now we do Y", finished plans, and paths that moved all confuse Claude a little each time.

A tune-up keeps what matters (your facts, preferences, and real rules) and removes the rest.

## Start here

Open Claude Code (any folder is fine) and paste this:

```
I want to run the tune-up from https://github.com/tysszl/claude-tuneup on my projects. Please install it and walk me through it.
```

Claude takes it from there. It installs the kit, finds your projects, and goes through them with you one at a time. Nothing in your files changes until you say yes, and everything is backed up first. Use Claude Opus 5.5 for this (type `/model opus` first); the judgment calls are the point.

Later, to tune up a project, open Claude Code in that project's folder and type `/tune-up`. You can also say what you want: `/tune-up my global setup` (your personal settings used everywhere) or `/tune-up the invoice skill`. Run it on each project once, then again every few months or after a new model comes out.

## For Claude: setting someone up

The person who sent you here is probably not a programmer. Run the commands yourself instead of asking them to, explain what you are doing in plain words, and ask before changing anything.

1. **Install.** Run `claude plugin marketplace add tysszl/claude-tuneup`, then `claude plugin install tune-up@tyler-tune-up`. If `claude` is not on the PATH, have them type `/plugin marketplace add tysszl/claude-tuneup` and then `/plugin install tune-up@tyler-tune-up` themselves. Offer to turn on auto-update for the `tyler-tune-up` marketplace (in `/plugin`, under marketplaces) so improvements reach them.
2. **Load it now.** The `/tune-up` command appears only after Claude Code restarts. To start without a restart, read `skills/tune-up/SKILL.md` from the installed copy (`claude plugin details tune-up@tyler-tune-up` shows where it is, usually under `~/.claude/plugins/`) or from this repository, and follow it, reading its `references/` files as it directs.
3. **Find their projects.** Look for folders with a `CLAUDE.md`, `AGENTS.md`, or `.claude/` folder in the current folder and the usual places (home folder, `~/Documents`, `~/Desktop`, `~/Projects`, `~/code`). Show them a short list with the last time each was changed, and suggest an order: their global setup (`~/.claude/`) first, since it affects every project, then the projects they use most.
4. **One at a time.** Tune up the first one now. For each next one, suggest a fresh session: quit, open Claude Code in that project's folder, and type `/tune-up`. A fresh session per project keeps each run accurate and cheaper.
5. **Settings.** When the tune-up reaches settings, walk them through the recommendations in `skills/tune-up/references/settings.md`, one plain sentence each, and change only what they approve.

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

## Auto memory

Claude Code keeps its own notes about you and each project ("auto memory") and reads them at the start of every session. That's how it remembers corrections you gave it last week. The catch: you never see those notes, so wrong or outdated ones stick around; they can contradict your `CLAUDE.md`; and they live only on your computer, outside your project folder and its backups.

Each tune-up reads those notes, moves the ones worth keeping into your `CLAUDE.md` where you can see them, and deletes the rest. It then asks whether you want auto memory on or off:

- **Keep it on** if you rarely edit `CLAUDE.md` yourself. Run a tune-up every few months to clean it up.
- **Turn it off** if you'd rather say "add this to CLAUDE.md" whenever you want Claude to remember something. Your notes then all live in one place you can read.

You can check what it has saved anytime with `/memory`.

## Habits that save usage

- **One task per session.** When you switch to something unrelated, type `/clear`. Long sessions make every message cost more.
- **Don't switch models or turn plugins on and off mid-session.** Claude Code reuses the unchanged part of the conversation at a discount, for about an hour. Switching models or tools throws that discount away.
- **Back after more than an hour?** The discount has expired. If the session was long, ask Claude for a short summary of where things stand, type `/clear`, and paste the summary in.
- **Raise effort only when needed.** `/effort high` for a hard problem; the default is fine for most work.
- **Look before guessing.** `/context` shows what's filling Claude's memory, `/usage` shows how much you're using, and `/skill-doctor` shows which skills you never use.
