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

A few short paragraphs or sections: purpose and audience, key facts and preferences, where things live, how to do the common tasks (or which skill does them), and hard boundaries. Often under 3 KB for a personal project. Length is not the goal; a file that is long because it holds true, needed facts is fine.

## Memory

If auto-memory is on, notes accumulate in `~/.claude/projects/<project-path>/memory/`. The index loads every session. Remove notes that are wrong, duplicated in `CLAUDE.md`, or about finished work. Promote a note that is a durable project fact into `CLAUDE.md` and delete the note. Tell the person whether auto-memory is on; see [settings](settings.md).

## Other files it loads

Follow every "read X on start" instruction and every `@` import. Anything read on every start must be needed on every start. Large reference docs (price lists, style guides, transcripts) should be pointed to, not imported.
