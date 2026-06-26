
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

Voice notes are recorded in real time, unedited, unfiltered, in English by a French native speaker. They land in a Notion archive called Blabbing about AI.

A Claude extraction skill runs daily. It reads new entries, identifies emotional beats using a breach-based definition grounded in Bruner and Burke's narrative theory, and extracts structured records. Each record contains an emotion label, Russell Circumplex coordinates, a verbatim quote, a job to be done, activity type, complexity score, and theme tags.

Records are appended to `data/corpus.json` on this repo, append-only, never rewritten. The corpus grows. At sufficient volume, phase boundaries will emerge from density patterns in the data.

Two frontend views are planned: a journey map (chronological emotional curve) and a galaxy view (theme-based clustering, no fixed axis).

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
