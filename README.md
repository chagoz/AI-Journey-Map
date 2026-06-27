# AI Journey Map

A longitudinal field study of one designer's evolving relationship with AI, built using the same tools it documents.

*The loop eating the loop.*

---

## What this is

A public research artifact. Not a productivity log. Not a portfolio. A structured record of how one person's relationship with an unfamiliar technology develops over time, captured in real time, processed with rigorous extraction rules, and made visible as data.

The raw input is voice notes recorded across commutes, walks, and workdays. The output is a growing corpus of emotional beats, each one a moment where the narrator's prior model of the tool was breached, positively or negatively. The data accumulates. Patterns emerge. Phases will eventually be declared by the corpus itself, not by the narrator.

The subject is the relationship between a person and a technology. Not the person's productivity. Not the technology's capabilities. The relationship itself.

---

## Why this exists

The narrator is a designer with over fifteen years of cross-disciplinary practice spanning brand, UX, product, and AI-assisted workflows. She works at the intersection of systems thinking and creative practice, building things that did not exist before, then teaching others how to build them.

When AI tools became genuinely useful in her daily work, she noticed something worth documenting: the adoption was not smooth or linear. It was full of breaches, moments where the technology did something she did not expect, revealed something about her own limits, or changed how she understood what she was doing. Those moments felt like data. So she started collecting them.

The project is also an experiment in methodology: can AI be used to process and structure a corpus about AI adoption without introducing the very biases it is meant to document? The extraction rules and anti-inference constraints are the answer in progress.

---

## How it works

Voice notes are recorded in real time, unedited, unfiltered, in English by a French native speaker. They land in a Notion archive called Blabbing about AI — a single page where transcripts are stored as recorded, untouched after the fact.

A Claude extraction skill runs daily. It reads new entries, identifies emotional beats using a breach-based definition grounded in Bruner and Burke's narrative theory, and extracts structured records. Each record contains an emotion label, Russell Circumplex coordinates, a verbatim quote, a job to be done, activity type, complexity score, and theme tags.

Records are appended to `data/corpus.json` on this repo, append-only, never rewritten. The corpus grows. At sufficient volume, phase boundaries will emerge from density patterns in the data.

Two frontend views are planned: a journey map (chronological emotional curve) and a galaxy view (theme-based clustering, no fixed axis).

---

## The extraction skill

The extraction skill is the automated engine of this project. It runs daily via a Cowork scheduled task and handles the full loop from raw voice note to committed corpus record, with no human involvement in the data processing.

### What it does

Reads new entries from the raw voice note archive in Notion — in this project called Blabbing about AI, a page where unedited transcripts are stored as they are recorded, untouched after the fact. Compares against the existing corpus to identify unprocessed entries. Applies the extraction rules and anti-inference constraints defined in `docs/extraction-rules.md`. Outputs structured beat records and commits them directly to `data/corpus.json` via the GitHub API. Logs each run to the project changelog in Notion.

### Human vs Claude role

This distinction is intentional and load-bearing for the study's integrity.

The human records voice notes in real time, unedited, unfiltered, with no awareness of what will be extracted. The human does not categorise, tag, or interpret the entries. The human does not review beats before they are committed.

Claude reads the rules, identifies beats, extracts all fields, assigns emotion coordinates, applies theme tags, and commits to GitHub. Claude does not receive editorial input from the human at any point in the extraction loop. The human's only interaction with the corpus is through the public-facing artifact.

This separation is what makes the study methodologically honest. If the narrator also curates the data, the study becomes a highlight reel.

### Setup requirements

To run this skill yourself:

1. Create a Cowork project in Claude Desktop and sync it to your forked GitHub repo — this gives the skill access to your docs and corpus
2. Add your GitHub personal access token to the Cowork project instructions as `GITHUB_TOKEN` and your repo name as `GITHUB_REPO` — these are never written to any file
3. Upload `docs/SKILL.md` to your Cowork project as a custom skill
4. Create a scheduled task in Cowork pointing to the skill, daily at a time when your computer is awake and Claude Desktop is open
5. Set up your raw voice note archive in Notion as a single page where transcripts land unedited. Connect the Notion connector to your Cowork project and make sure the skill can find the page by name. In this project that page is called Blabbing about AI — name yours whatever makes sense, but update the skill's Step 3 to point to the right page name

The skill reads all rules from your GitHub docs folder on every run. When you update a rule, the next extraction automatically uses the new version.

---

## Methodology

This project draws on:

**Jerome Bruner and Kenneth Burke** for the definition of a beat: a unit of experience bounded by a breach of canonical expectation, with both a landscape of action and a landscape of consciousness.

**Roger Silverstone's domestication theory** as the orienting framework for the theme taxonomy, describing how individuals appropriate, objectify, incorporate, and convert new technologies.

**James Pennebaker's LIWC methodology** as the anchor for emotion labelling: linguistic markers in the verbatim as evidence of psychological state, not self-reported feeling.

**James Russell's Circumplex Model** as a validation layer: every emotion label is plotted on valence and arousal axes to catch labelling drift over time.

Full methodology is documented in `docs/methodology.md`.

---

## A note on bias

This is a declared field study, not a neutral record. The following are known variables, not hidden assumptions.

The narrator has a prior positive disposition toward AI. Her professional identity is oriented around building and systems-thinking. She works in English as a second language, with French as her primary cognitive register, a tracked variable across the corpus.

The extraction skill introduces a second layer of interpretation. The rules in `docs/extraction-rules.md` constrain this as tightly as possible. Judgment calls remain.

This project does not claim objectivity. It claims honesty about its constraints.

---

## Repository structure

```
data/
  corpus.json          — the live corpus, append-only

docs/
  methodology.md       — intellectual foundations, theoretical anchors
  extraction-rules.md  — mechanical rules governing extraction
  schema.md            — field-by-field reference
  taxonomy.md          — theme definitions, application rules, linguistic anchors
  changelog.md         — all rule changes and schema versions, dated
  SKILL.md             — the extraction skill, ready to upload to Cowork
```

---

## Want to fork this?

The methodology is designed to be replicable. A template repo with an empty corpus, sample beats, and the full docs is available at:

[github.com/chagoz/AI-Journey-Map-Template](https://github.com/chagoz/AI-Journey-Map-Template)

Fork it. Set up your own voice note archive. Run the extraction skill against your own entries. The methodology is yours to adapt.

---

## About

Built by [Charline Vergoz](https://www.linkedin.com/in/charlinevergoz/) — designer, educator, systems thinker.

*Created June 2026. Corpus updated daily.*
