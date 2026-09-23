# Usage-saving settings

Read `~/.claude/settings.json` (and the project's `.claude/settings.json` if any). Recommend only what applies, explain each in one plain sentence, and change a setting only when the person approves it. Setting names change between versions: confirm against `claude --help` or https://code.claude.com/docs/en/settings before editing, and keep the file valid JSON.

| Setting | Recommendation | Why |
|---|---|---|
| `env.CLAUDE_CODE_AUTO_COMPACT_WINDOW` | `"400000"` on 1M-context models | Every turn resends the whole conversation. Summarizing at 400k instead of near 1M keeps long sessions much cheaper, and quality drops in very long contexts anyway. Per-session: `claude --autocompact 400k`. |
| `effortLevel` | Leave at the model default (`medium` on Opus 5.5) unless they set it higher for everything | Higher effort thinks longer on every turn. Raise it per task with `/effort high` when a task is hard. |
| `autoMemoryEnabled` | Their choice, after the memory review in [instructions](instructions.md) §Auto memory. `false` turns it off everywhere; set it in a project's `.claude/settings.json` to turn it off for one project | Memory loads every session and is hidden, machine-local, and prone to stale or conflicting notes; it is also how corrections get remembered for people who don't edit `CLAUDE.md`. |
| Plugins in `enabledPlugins` | Turn off plugins they don't use | Each enabled plugin adds skills to the list every turn. |
| MCP servers | Remove servers they don't use | Tool search defers most tool detail, but each server still adds names and startup time. |

## Habits to pass on (no setting)

- **One task per session.** Start fresh with `/clear` when switching to unrelated work. A long session makes every later message cost more.
- **Keep the cache warm.** Claude Code reuses the unchanged start of the conversation cheaply for about an hour on a subscription (five minutes on an API key). Switching models mid-session, turning plugins or MCP servers on or off, and `/compact` start the cache over. Pick the model and tools at the start and keep them.
- **Coming back after a break of more than an hour:** the cache has expired, so the next message pays full price for the whole conversation. For a large session, ask for a short summary of where things stand, then `/clear` and paste it, instead of continuing.
- **Look before guessing.** `/context` shows what fills the context window; `/usage` shows usage and cache hits; `/skill-doctor` shows which skills cost context and never get used.
