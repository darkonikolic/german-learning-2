---
name: extract-german-vocabulary
description: Extracts B1-level German vocabulary from user-written texts and distributes words into vocabulary files by type (nouns, verbs, adjectives, etc.). Use when the user asks to extract words from a text, pull vocabulary from texts/, or process German texts for learning.
---

# Extract German B1 Vocabulary

## Purpose

When the user provides a German text or points to `texts/`, extract vocabulary appropriate for B1 level and save each word to the correct file in `vocabulary/` by word type.

## Workflow

1. **Read the text** – from user message or from `texts/*.md`
2. **Identify words** – all content words (skip pure A1 basics like "ich", "und", "ist" unless contextually important)
3. **Classify by type** – Substantiv, Verb, Adjektiv, Adverb, Präposition, or Andere
4. **Filter for B1** – focus on B1-relevant vocabulary (everyday, work, health, travel, education, society)
5. **Write to files** – append to existing `vocabulary/[Type].md` file (no subfolders)

## File Mapping

| Type | Path |
|------|------|
| Substantiv | vocabulary/Substantive.md |
| Verb | vocabulary/Verben.md |
| Adjektiv | vocabulary/Adjektive.md |
| Adverb | vocabulary/Adverbien.md |
| Präposition | vocabulary/Präpositionen.md |
| Konjunktion, Partikel, Pronomen | vocabulary/Andere.md |

**No subfolders** – one file per type, words sorted alphabetically.

## Output Format

Each vocabulary file. Words sorted alphabetically. Format per word:

```markdown
# [Type]

## {word}

[sr] {Serbian translation}
[en] {English translation}

```

- **Substantive**: heading with article – `## der Arbeit`, `## die Kunst`
- **Verben**: infinitive only. Verb tenses extracted separately – not in vocabulary.
- **Translations**: [sr] Serbian, [en] English
- **Sort**: alphabetically (ABC)
- Empty line between each word block

## Deduplication

Before adding a word, check if it already exists in the target file. If the file exists, merge new words without duplicates.

## B1 Scope

B1 vocabulary includes: work/career, health, daily life, society, education, travel, common adjectives (flexibel, zuverlässig), verbs (vergleichen, vorbereiten, verbessern), connectors (deshalb, trotzdem, außerdem).
