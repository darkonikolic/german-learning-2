# German Learning (A1→B1)

Project for learning German. Lekcije (evidencija časova), Readle (vežbe), praktika, vocabulary extraction, grammar.

**Cursor:** Agent automatski postavlja Attribution OFF. Vidi `.cursor/SETUP.md`.

## Structure

```
german-learning-02/
├── lekcije/                  # Evidencija časova (kurs – jedan fajl po lekciji)
│   ├── A1/
│   ├── A2/
│   └── B1/
├── readle/                   # Readle vežbe (format: Y-m-d_H:i_title.md)
├── praktika/                 # Beleške iz praktičnih sesija (Y-m-d.md)
├── standup/                  # Dnevni izveštaji na 3 jezika (Y-m-d.md)
├── themen/                   # Teme po grupama (grammatik, alltag, arbeit...)
├── vremena/                  # Verb tenses (B1)
│   ├── Präsens.md
│   ├── Perfekt.md
│   ├── Präteritum.md
│   ├── Plusquamperfekt.md
│   ├── Futur-I.md
│   └── Futur-II.md
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

## Text Format in readle/

Each file in `readle/` has format:

```markdown
# [Title]

[Y-m-d]
```

User writes content below. New files are created empty (title + date only).

## Lekcije (Evidencija časova)

1. **Piši belške** u `lekcije/A1/1-1.md` tokom časa
2. **Kaži AI**: "Ispravi i izvuci reči i gramatiku iz lekcije 1-1" ili "iz A1/1-1"
3. AI ispravlja gramatiku inline (gde god pišeš), dodaje prevode u Prevodi [DE] [SR] [EN], izvlači reči u `vocabulary/`, beleži gramatiku

## Organizacija

| Aktivnost | Folder | Format |
|-----------|--------|--------|
| Kurs (predavanja) | lekcije/ | Belške, Prevodi, Gramatika, Reči, Izvor |
| Readle (vežbe) | readle/ | Y-m-d_H:i_title.md |
| Praktika (razgovor, vežbanje) | praktika/ | Y-m-d.md – beleške po sesiji |
| Standup (dnevni izveštaji) | standup/ | Y-m-d.md – [DE] [SR] [EN] po pasusu |

## How to Use (Texts)

1. **Write a text** in `readle/` – file format `Y-m-d_H:i_title.md` (e.g. `readle/2025-03-10_14:30_mein-tag.md`)
2. **Request extraction** – tell AI: "Extract B1 words from text X" or "Extract B1 vocabulary from readle/"
3. AI will extract B1-level words and distribute them to the appropriate files in `vocabulary/`

## Vocabulary File Format

One file per type. Words sorted alphabetically. Format per word:

```markdown
## {word}

[sr] {Serbian}
[en] {English}

```

## B1 Level

B1 (CEFR) covers ~2500–3000 words for everyday communication: work, health, travel, education, society.
