# Dated patterns

Instructions written for older models often carry habits that current models do not need, and some now hurt: they cause over-caution, needless questions, or rigid behavior. Grep the files in scope for these. A hit is a candidate, not a verdict.

| Pattern | Look for | Usual fix |
|---|---|---|
| Shouting | `MUST`, `NEVER`, `ALWAYS`, `CRITICAL`, `IMPORTANT` in caps, `!!`, bold warnings with no reason | State the rule plainly with its reason. Current models over-apply shouted rules. |
| Hedged requirements | `try to`, `if possible`, `ideally` on things that are actually required | State it as a requirement, or drop it if it is not one. |
| Reasoning recipes | `think step by step`, `<thinking>` or `<scratchpad>` tags, "first analyze, then plan, then..." for judgment work | Remove; the model reasons on its own. Keep order only where it protects something. |
| Personas | `You are an expert...`, `You are a world-class...` | Replace with the facts that expert would know about this person's situation, or remove. |
| Repetition | `Remember,`, `Again,`, `As stated above`, the same rule in several files | Say it once in the right place. |
| Chains of don'ts | Three or more `Do not`/`Never`/`Avoid` in a row | Keep prohibitions tied to a real past failure or real risk; turn the rest into one statement of the goal. |
| Output suppressors | `don't explain`, `no bullet points`, `never use headers`, `only output X` where no program reads the output | Remove or narrow to where the format truly matters. |
| Fossils | Old model names (Claude 3, Sonnet 3.5, GPT-4), `no longer`, `now we`, `instead of the old`, dated `Update:` notes | Restate the current rule as if it were always the rule. |
| Word counts | `at most N words`, `every N messages remind` | Describe the length or cadence wanted in plain terms. |
| Long required reading | "Before anything, read A, B, C, and D" | Load each only for the task that needs it. |

## Keep

Facts are never cruft. Exact formats that another program or person depends on stay. Rules that prevent a real, demonstrated problem stay. A short line of who the assistant is for is fine. Cruft is not the same as length.

## If a removal might matter

Removing an instruction is a guess until tested. When a cut touches something with real stakes, try a representative task before and after (a fresh subagent works), and put the rule back in shorter form if behavior gets worse.
