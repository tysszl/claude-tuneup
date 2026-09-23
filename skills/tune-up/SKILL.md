---
name: tune-up
description: Audit and refactor a project's CLAUDE.md, skills, and Claude Code settings for accuracy, clarity, and lower usage; use when asked to tune up, clean up, or audit a setup.
---

# Tune-up

Make a Claude Code setup that a fresh session can work from with less reading, fewer wrong turns, and no stale claims. Many setups were written for older models that needed heavy scaffolding: rigid step lists, ALL-CAPS warnings, repeated rules, and history of how things used to work. Current models do better with a clear purpose, true facts, real boundaries, and pointers to detail they load only when needed.

The person running this is usually not a programmer. They cannot review a diff, so the plain-language summary and the backup are their protection.

## Scope

Pick the scope from the request; ask only if it is unclear.

| Request | Covers |
|---|---|
| This project (default) | `CLAUDE.md`, `CLAUDE.local.md`, `.claude/rules/`, `.claude/skills/`, `.claude/settings*.json`, any files `CLAUDE.md` says to read, and the auto-memory folder for this project if it exists |
| My global setup | `~/.claude/CLAUDE.md`, `~/.claude/skills/`, `~/.claude/settings.json` |
| One skill | That skill's folder |

Skills installed by a plugin live under `~/.claude/plugins/` and are owned by someone else. Report problems with them; do not edit them. A plugin skill that is never used can be turned off instead.

## Work

1. **Inventory and measure.** List every file in scope with its size. Work out what loads on every session (instruction files, imported `@` files, skill descriptions) versus what loads only when needed. Estimate tokens as bytes ÷ 4; the person can confirm with `/context`.
2. **Audit.** Read [instructions](references/instructions.md) for instruction files and memory, [skills](references/skills.md) for skills, [dated patterns](references/cruft-signals.md) for both, and [settings](references/settings.md) for configuration. Check facts against the real project: paths exist, commands run, names match.
3. **Report.** Give the person a short plain-language summary: what you would change and why it helps them, grouped as *remove*, *rewrite*, *move*, *fix*, and *keep*. Include before and after size of what loads every session. List anything you are unsure about as a question, not a change. Settings changes are listed separately because they affect every project.
4. **Back up, then apply** what they approve. One approval covers the whole approved list; do not re-ask per file. Before the first edit, make the work recoverable: in a Git repo, commit the current state with the message `Before tune-up`; otherwise copy every file you will change into `~/.claude/tune-up-backups/<YYYY-MM-DD-HHMM>/`, keeping folder structure. Tell them where the backup is.
5. **Check the result.** Start a subagent with no prior context. Have it read only the new setup and answer three or four questions a real session here would need (what is this project, where does X live, how do I do the most common task, what must never happen). Compare its answers against the originals. Restore anything it could not find.
6. **Finish** with what changed, the every-session size before and after, the backup location, and how to undo (`git reset --hard HEAD~1` right after, or copy the backup back). Suggest starting a new session so the changes load.

## Boundaries

- Keep facts, preferences, names, accounts, safety rules, and anything about people or money unless the person confirms it is wrong or no longer needed. When unsure, keep it and ask.
- Do not change what the project does, only how it is described to Claude.
- Change settings only when the person approves that specific setting.
- Do not delete a skill that has uses without asking. Offer "manual only" (it stays available by name but stops costing context every turn) as the middle option.
- Never push to a remote, send anything, or touch files outside the scope.
