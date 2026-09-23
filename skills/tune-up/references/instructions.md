# Instruction files and memory

`CLAUDE.md` loads into every session in its folder, along with every file it imports with `@path`. Every line costs tokens on every turn and competes for attention. Its job is what a capable newcomer could not work out alone: what the project is for, who it serves, true facts and preferences, real boundaries, and where things live.

## Ask of every section

- **Could Claude work this out on its own?** Generic advice ("be thorough", "write clean code", "think carefully") and descriptions of files Claude can simply read are removal candidates.
- **Is it still true?** Check paths, commands, names, dates, counts, and statuses against the real project. Correct the file to match reality unless the text records a decision.
- **Is it needed every session?** Detail used for one kind of task moves to a separate file that `CLAUDE.md` points to by task ("For invoices, read `docs/invoices.md`"), or into a skill. Leave what every session needs in place. A pointer must name when to read the file.
- **Is it said once?** Keep each rule in one place. Remove repeats across `CLAUDE.md`, rules files, skills, and memory; keep the copy in the most specific home.
- **Is it history?** "We used to...", "As of March...", "Update:", finished plans, and changelogs belong in Git or nowhere. Rewrite live rules in present tense. Keep a date only when someone must recheck it or it marks when a permission was given.
- **Is it a real rule or a nervous one?** A rule that protects something real (money, other people, sending messages, deleting data, privacy) stays, stated plainly with its reason. Emphasis without a reason ("CRITICAL", "NEVER EVER") gets restated calmly.

## Shape of a good CLAUDE.md

A brief statement of purpose and audience, then most of the words on what would trip up a capable newcomer: gotchas, non-obvious facts and preferences, where things live, which skill handles which task, and hard boundaries. Stay well under 200 lines; for a personal project, often under 3 KB. Length is not the goal; a file that is long because it holds true, needed facts is fine.

Guidance that applies only to certain files can move to `.claude/rules/<topic>.md` with a `paths:` list in its frontmatter (for example `paths: ["invoices/**"]`), so it loads only when Claude works on matching files. Rules files without `paths:`, and files using other tools' keys such as `globs:`, load every session. Check the current format at https://code.claude.com/docs/en/memory before writing one.

Instructions are guidance, not enforcement. If something must never happen (deleting a folder, sending from an account), tell the person a hook can block it outright, and offer to set one up.

## Auto memory

Auto memory is on by default. Claude saves notes about the person, their corrections, ongoing work, and where to find things in `~/.claude/projects/<project>/memory/`, and the `MEMORY.md` index loads every session (up to 200 lines). Current versions skip what the code or `CLAUDE.md` already says and prompt Claude to prune the index, so it is much less bloated than it once was. Its remaining weaknesses:

- **Invisible.** Most people never read it, so wrong or outdated notes persist unnoticed.
- **Stale work notes.** Notes about deadlines and in-progress work outlive the work.
- **Conflicts.** When `CLAUDE.md` changes, older notes can contradict it, and Claude cannot tell which wins.
- **One computer only.** Not in the project folder, not in Git, not backed up, and not seen on another machine or by a collaborator.

Review it every tune-up. For each note: move durable facts and preferences into `CLAUDE.md` (or a skill, if task-specific) and delete the note; delete notes that are wrong, finished, or already covered; leave current work notes. Report what moved and what was deleted.

Then ask whether they want to keep it on. Recommend keeping it on for someone who rarely edits `CLAUDE.md` themselves, since it is how their corrections get remembered, with a tune-up every few months to move the good parts into `CLAUDE.md`. Recommend turning it off for someone who prefers to say "add this to CLAUDE.md" when something should stick. Either is reasonable; see [settings](settings.md).

## Other files it loads

Follow every "read X on start" instruction and every `@` import. Anything read on every start must be needed on every start. Large reference docs (price lists, style guides, transcripts) should be pointed to, not imported.
