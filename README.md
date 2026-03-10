# German Learning (B1)

Project for learning German at B1 level. Structure allows writing texts and automatic word extraction by type.

## Structure

```
german-learning-02/
├── texts/                    # Your texts (format: Y-m-d_H:i_title.md)
├── vocabulary/               # Extracted words by type (one file per type)
│   ├── Substantive.md        # Nouns (der/die/das)
│   ├── Verben.md             # Verbs (infinitive only)
│   ├── Adjektive.md          # Adjectives
│   ├── Adverbien.md          # Adverbs
│   ├── Präpositionen.md      # Prepositions
│   └── Andere.md             # Other (conjunctions, particles, pronouns)
├── .cursor/
│   ├── rules/                # AI rules
│   ├── skills/               # Word extraction skill
│   └── AGENTS.md             # Agent configuration
└── README.md
```

## Text Format in texts/

Each file in `texts/` has format:

```markdown
# [Title]

[Y-m-d]
```

User writes content below. New files are created empty (title + date only).

## How to Use

1. **Write a text** in `texts/` – file format `Y-m-d_H:i_title.md` (e.g. `texts/2025-03-10_14:30_mein-tag.md`)
2. **Request extraction** – tell AI: "Extract B1 words from text X" or "Extract B1 vocabulary from texts/"
3. AI will extract B1-level words and distribute them to the appropriate files in `vocabulary/`

## Vocabulary File Format

One file per type. Words grouped by source. Translations in Serbian. Verbs in infinitive only:

```markdown
# [Type]

## [text-name]

| Word | Article | Translation | Example |
|------|---------|-------------|---------|
| Arbeit | die | work | Ich gehe zur Arbeit. |
```

## B1 Level

B1 (CEFR) covers ~2500–3000 words for everyday communication: work, health, travel, education, society.
