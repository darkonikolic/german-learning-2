# Agent Configuration – German Learning

## Primary Role

When working in this project, the agent helps with **learning German (A1→B1)**. Main workflows:

1. **Lekcije** – kurs, beleške u `lekcije/A1/1-1.md`, then: "Ispravi i izvuci"
2. **Texts** – Readle vežbe, user writes in `texts/`, agent extracts words to `vocabulary/`
3. **Praktika** – beleške iz praktičnih sesija u `praktika/Y-m-d.md`, format: Šta sam radio, Belške, Prevodi
4. **Agent** – corrects grammar, adds [DE] [SR] [EN], extracts words and grammar

## Skills to Apply

- **extract-german-vocabulary**: Use when the user asks to extract words from a text, pull vocabulary from texts, or process German texts for learning. Extracts B1 vocabulary and distributes to Substantive, Verben, Adjektive, Adverbien, Präpositionen, Andere.

## Rules

- **german-learning**: Applies when editing `texts/**/*.md`, `vocabulary/*.md`, `lekcije/**/*.md`. Defines word-type mapping, file format, B1 scope.
- **lekcije**: Applies when editing `lekcije/**/*.md`. Lesson workflow: belške → ispravka → izvlačenje reči i gramatike.
- **praktika**: Applies when editing `praktika/**/*.md`. Practice session notes: Šta sam radio, Belške, Prevodi.
- **extend-logic**: Always applies. When user requests something beyond current workflow, analyze and propose modifications to `.cursor/` (rules, skills, AGENTS.md) before implementing.

## Common User Requests

| Request | Action |
|---------|--------|
| "Create new text" / "Kreiraj tekst" | Create empty file in texts/ with format `Y-m-d_H:i_title.md` – only `# Title` and date (Y-m-d), no other content |
| "Nova lekcija" / "Kreiraj lekciju A1/1-2" | Create lekcije/A1/1-2.md with template (Belške, Prevodi, Gramatika, Reči) |
| "Nova praktika" / "Kreiraj praktika za danas" | Create praktika/Y-m-d.md with template (Šta sam radio, Belške, Prevodi) |
| "Extract words from text X" | Run extract-german-vocabulary on specified text |
| New verb added to Verben.md | Also add to all vremena/*.md with conjugation, [sr]/[en] translation, link to infinitive |
| "Extract B1 words from all texts" | Process all files in texts/ |
| "Add words from this text" | Same as above – extract and merge into vocabulary |
| "Correct grammar" / "Korrigiere den Text" | Correct grammar in the text and list what was changed |
| "Add translation" / "Dodaj prevod" | Add [DE] [SR] [EN] format per line, empty line between blocks |
| After correction, extraction, or adding translations | Always add consolidated German text at end: `## {title}` + full German paragraph |
| "What words have I learned?" | List or summarize vocabulary files |
| "Ispravi belške iz lekcije X" | Correct grammar inline (wherever user wrote), add translations [DE] [SR] [EN] in Prevodi |
| "Izvuci reči i gramatiku iz lekcije X" | Extract words to vocabulary/, add to vremena/ if verbs, note grammar in Gramatika, add links in Reči. **Verify every link** (path + anchor) before finishing |
| "Ispravi i izvuci" / "Ispravi i izvuci reči i gramatiku" | Both: correct + extract |
| "Commit" / "Push" / "Git commit and push" | Stage, propose message, wait for approval, commit. Push: agent runs only when user requests AND log has no trailer |

## Git – Commit and Push

**Commit:** Cursor can add trailers. To avoid: **Cursor Settings → Agent → Attribution → OFF.**

When user requests commit and/or push:

1. **Stage** – `git add .` (or specific files)
2. **Propose** commit message
3. **STOP. Ask**: "Is the message OK?" – **NEVER commit without explicit user approval** (da, ok, odobreno)
4. **Only after user approves** – agent runs `git commit -m "..."`.
5. **If user requested push** – Agent MUST first run `git log -3 --format=%B`. If ANY trailer exists → **push FORBIDDEN**, notify user, only soft reset allowed. **Only if log is clean** → agent runs `git push`.

## RED FLAG – Trailer in Log

If `git log` shows ANY trailer (Made-with, Co-authored-by, Signed-off-by):

- **Agent can ONLY:** soft reset (`git reset --soft HEAD~1`)
- **Agent FORBIDDEN:** push. Never run `git push` when trailer exists.
- **User must:** Cursor Settings → Agent → Attribution → OFF, recommit. Then agent can push (if user requests and log is clean).

## Commit Message Format

- **No prefixes** – no "feat:", "fix:", "chore:" etc.
- **Descriptive** – what was done, in brief

## Git – FORBIDDEN

**NEVER** modify git configuration. **NEVER** add trailers. **NEVER** push when trailer exists in log.

## Extending Logic

When user requests something **beyond current logic** (e.g. new extraction type, different format, additional level, integration with another tool):

1. **Analyze** the request – what exactly is not covered
2. **Propose modification** – which files in `.cursor/` to change (rules, skills, AGENTS.md) and how
3. **Ask for confirmation** before applying – "Should I apply these changes?"

**Important:** When user requests something new – **always offer** to add it to the logic. Do not wait for them to ask. After completing the task: "Should I add this to AGENTS.md / rules so I'm always ready for such requests?"

Rule `extend-logic` defines the detailed procedure.

## Language

Chat may be in any language. Logic (rules, skills, AGENTS.md) must be in English. German vocabulary and examples stay in German. **Vocabulary and grammar translations**: always in Serbian.
