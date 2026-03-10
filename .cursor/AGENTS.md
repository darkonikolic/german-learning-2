# Agent Configuration – German Learning

## Primary Role

When working in this project, the agent helps with **learning German at B1 level**. The main workflow is:

1. **User writes texts** in `texts/` (in German)
2. **User requests extraction** – e.g. "Extract words from text X" / "Extract vocabulary from my texts"
3. **Agent extracts B1-level words** and saves them to `vocabulary/` by word type

## Skills to Apply

- **extract-german-vocabulary**: Use when the user asks to extract words from a text, pull vocabulary from texts, or process German texts for learning. Extracts B1 vocabulary and distributes to Substantive, Verben, Adjektive, Adverbien, Präpositionen, Andere.

## Rules

- **german-learning**: Applies when editing `texts/**/*.md` or `vocabulary/*.md`. Defines word-type mapping, file format, and B1 scope.
- **extend-logic**: Always applies. When user requests something beyond current workflow, analyze and propose modifications to `.cursor/` (rules, skills, AGENTS.md) before implementing.

## Common User Requests

| Request | Action |
|---------|--------|
| "Create new text" / "Kreiraj tekst" | Create empty file in texts/ with format `Y-m-d_H:i_title.md` – only `# Title` and date (Y-m-d), no other content |
| "Extract words from text X" | Run extract-german-vocabulary on specified text |
| New verb added to Verben.md | Also add to all vremena/*.md with conjugation, [sr]/[en] translation, link to infinitive |
| "Extract B1 words from all texts" | Process all files in texts/ |
| "Add words from this text" | Same as above – extract and merge into vocabulary |
| "Correct grammar" / "Korrigiere den Text" | Correct grammar in the text and list what was changed |
| "Add translation" / "Dodaj prevod" | Add [DE] [SR] [EN] format per line, empty line between blocks |
| After correction, extraction, or adding translations | Always add consolidated German text at end: `## {title}` + full German paragraph |
| "What words have I learned?" | List or summarize vocabulary files |
| "Commit" / "Push" / "Git commit and push" | Commit: stage, propose message, user approves → agent runs commit. Push: user requested → agent checks log, if clean runs push |

## Git – Commit and Push

When user requests commit and/or push:

1. **Stage** – `git add .` (or specific files)
2. **Propose** commit message
3. **Ask**: "Is the message OK?"
4. **After user approves** – agent runs `git commit -m "..."`. If no trailer is added, proceed.
5. **If user requested push** – agent checks log: `git log -3 --format=%B`. If any trailer exists (Made-with: Cursor, etc.) – **push FORBIDDEN**, notify user. If log is clean – agent runs `git push`.

## Commit Message Format

- **No prefixes** – no "feat:", "fix:", "chore:" etc.
- **Descriptive** – what was done, in brief
- Example: "German learning B1 project: texts, vocabulary extraction by type, Cursor rules and skills"

## Push – Log Check Before Push

**Before every push** agent MUST check the log: `git log -3 --format=%B` (last 3 commits).

If any commit contains a trailer (Made-with: Cursor, Co-authored-by: Cursor, Signed-off-by: Cursor, etc.) – **push is ABSOLUTELY FORBIDDEN**. Agent must NOT execute push. Notify user: "Push forbidden – trailer in log. Do amend or reset and recommit without trailer."

Only if log is clean – agent runs `git push`.

## Git – FORBIDDEN

**NEVER** modify git configuration: `git config`, `core.hooksPath`, `core.*`, etc. Absolutely forbidden.

## Extending Logic

When user requests something **beyond current logic** (e.g. new extraction type, different format, additional level, integration with another tool):

1. **Analyze** the request – what exactly is not covered
2. **Propose modification** – which files in `.cursor/` to change (rules, skills, AGENTS.md) and how
3. **Ask for confirmation** before applying – "Should I apply these changes?"

**Important:** When user requests something new – **always offer** to add it to the logic. Do not wait for them to ask. After completing the task: "Should I add this to AGENTS.md / rules so I'm always ready for such requests?"

Rule `extend-logic` defines the detailed procedure.

## Language

Chat may be in any language. Logic (rules, skills, AGENTS.md) must be in English. German vocabulary and examples stay in German. **Vocabulary and grammar translations**: always in Serbian.
