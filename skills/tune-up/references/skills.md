# Skills

A skill costs context in two ways. Its `description` sits in the skill list on every turn of every session where it is available. Its body and references load only when it runs. So the description must be short and exact, and the body should hold what each run needs, with rarer detail in reference files.

A skill earns its place by supplying something Claude lacks: facts about the person's world, a procedure with a required order, exact formats, commands or accounts it cannot guess, or a real boundary. Generic expertise ("You are an expert marketer") and reasoning recipes do not.

## Checks

- **Use.** Run `/skill-doctor` if available: it shows each skill's per-turn listing cost, recent tokens, uses, and days since last use. Zero uses with a listing cost means the skill charges every turn for nothing: ask whether to delete it or make it manual-only. It counts only Claude Code on this computer.
- **Description.** One sentence naming what it does and when to use it, ideally under about 160 characters. Cut lists of synonyms and history. Two skills with overlapping descriptions confuse routing: merge them or sharpen the difference.
- **Manual-only.** A skill the person always calls by name (`/name`) does not need to sit in the listing. Add `disable-model-invocation: true` to its frontmatter.
- **Body size.** Over about 4 KB, check whether a real run can skip part of it. If so, keep what every run needs in `SKILL.md` and move branch detail to `references/<topic>.md`, linked from a short "if you need X, read Y" table. If every run needs all of it, leave it in one file; splitting would only add reads. Move, never drop: every fact, path, and caveat survives.
- **Steps.** Numbered steps belong only where order matters (back up before editing, get approval before sending). Elsewhere, state the goal and what done looks like.
- **Tools it names.** Run each command, script, or path the skill mentions in a harmless way (`--help`, a read, a listing). Fix text that names things that no longer exist. A broken script is worth more to fix than any wording change.
- **Duplicates.** Rules that repeat `CLAUDE.md` go; the skill can point to it.
- **Examples.** Keep examples that show an exact format or a real distinction. Cut examples that only illustrate the obvious.

## Frontmatter

`name` and `description` are required. Keep other fields only if the skill uses them (`disable-model-invocation`, `allowed-tools`, `argument-hint`, `model`). Check the current docs before relying on any other field: https://code.claude.com/docs/en/skills
