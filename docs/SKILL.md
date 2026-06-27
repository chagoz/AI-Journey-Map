---
name: ai-journey-map-extraction
description: Extraction skill for the AI Journey Map project. Run this skill whenever new voice note entries need processing. Reads Blabbing about AI in Notion, compares against the live corpus on GitHub, extracts structured emotional beats from unprocessed entries following the rules in the GitHub docs folder, and commits new beats directly to GitHub via the API. Triggers on any phrase suggesting new entries need processing, or runs automatically on schedule at 09:00 daily.
---

# AI Journey Map — Extraction Skill v3

Fully cloud-based. Reads rules and corpus from GitHub. Reads entries from Notion. Writes beats back to GitHub via API. No local files required.

---

## Credentials

Read from project instructions:
- `GITHUB_TOKEN` — personal access token with repo scope
- `GITHUB_REPO` — `chagoz/AI-Journey-Map`

These are never written to any file or output.

---

## Source URLs

**Rules and docs (raw GitHub):**
- Methodology: `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/methodology.md`
- Schema: `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/schema.md`
- Extraction rules: `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/extraction-rules.md`
- Taxonomy: `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/taxonomy.md`

**Corpus (GitHub API):**
- `https://api.github.com/repos/chagoz/AI-Journey-Map/contents/data/corpus.json`

**Notion:**
- Blabbing about AI — use Notion connector

**Notion project log:**
- `https://app.notion.com/p/38a728a6b59f8129b97ce6f3026842d1`

---

## Step 1 — Read the rules

Fetch and read these four documents in order:

1. `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/methodology.md` — the intellectual foundation. Understand the beat definition, the hybrid emotion protocol, and the declared limitations.
2. `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/schema.md` — the field reference. Confirm field names, types, and constraints before extracting any record.
3. `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/extraction-rules.md` — the mechanical rules. Every field definition, every anti-inference rule, every edge case.
4. `https://raw.githubusercontent.com/chagoz/AI-Journey-Map/main/docs/taxonomy.md` — the theme taxonomy. Read the full definition and linguistic anchor for every tag before applying any.

Do not proceed until all four are read and confirmed. If any fetch fails, stop and log the failure to Notion.

---

## Step 2 — Fetch the current corpus

Fetch the corpus via GitHub API:

```
GET https://api.github.com/repos/chagoz/AI-Journey-Map/contents/data/corpus.json
Authorization: token {GITHUB_TOKEN}
Accept: application/vnd.github.v3+json
```

From the response:
- Decode the base64 `content` field to get the JSON array
- Store the `sha` value — required for the write step
- Identify the highest `entry_ref` value — last processed entry
- Identify the highest `beat_id` value — next beat starts from this number + 1
- Note total beats in corpus

If the corpus is empty, start from Entry 01 and beat_001.

---

## Step 3 — Read Blabbing about AI from Notion

Use the Notion connector to fetch the Blabbing about AI page.

List all entries. Compare against the last processed entry from Step 2. Identify all entries that come after it.

If no new entries exist, skip to Step 8. Log: *No new entries to process. Corpus is current.*

---

## Step 4 — Self-assessment declaration

Before extracting anything, output the mandatory declaration as defined in `extraction-rules.md` Step 3.

The declaration must include:
- Which entries will be processed
- Last processed entry
- Next beat_id
- One concrete example of each Rule A through E applied to the specific entries about to be processed

Do not begin extraction until this declaration is complete. If you cannot confirm all five rules with concrete examples, stop and log the failure to Notion.

---

## Step 5 — Extract beats

For each unprocessed entry, apply the full extraction rules from `extraction-rules.md`.

Key reminders:
- A beat opens on a breach of expectation, not an emotion shift
- The prior expectation must be stated or strongly implied within the entry itself
- Select the verbatim before writing the emotion label
- Derive `emotion_valence` and `emotion_arousal` from the label using the Russell grid — verify consistency before finalising
- Apply the scope test to every field
- Apply Rules A through E throughout — no inference beyond the text, no cross-entry contamination

If an entry produces no beats, log: *Entry [ref] — no qualifying beats extracted.* Continue to next entry.

If no entries produce any beats, skip to Step 8.

---

## Step 6 — Commit updated corpus to GitHub

Take the existing corpus array from Step 2. Append the new beats. Do not reorder or modify existing records.

Encode the updated array as base64. Push via GitHub API:

```
PUT https://api.github.com/repos/chagoz/AI-Journey-Map/contents/data/corpus.json
Authorization: token {GITHUB_TOKEN}
Accept: application/vnd.github.v3+json

{
  "message": "corpus: append [N] beat(s) -- [YYYY-MM-DD]",
  "content": "[base64-encoded updated corpus]",
  "sha": "[sha from Step 2]",
  "branch": "main"
}
```

Wait for confirmation. Store the commit URL from the response.

If the commit fails, stop. Do not retry automatically. Log the failure to Notion with the error details.

---

## Step 7 — Output extraction note

Output a summary after successful commit:

- Entries processed: [list]
- Beats extracted: [count]
- Total corpus after commit: [new total] beats
- Commit URL: [url]
- Ambiguous labels: [if any — exact text only]
- Theme candidate text: [if any — exact text and beat reference only, no proposed label]

---

## Step 8 — Log to Notion project log

Append a run entry to the changelog section of the Notion project log.

**If new beats were extracted and committed:**
`[YYYY-MM-DD]` — Extraction run complete. Entries processed: [list]. Beats extracted: [count]. Total corpus: [new total] beats. Commit: [URL].

**If no new entries were found:**
`[YYYY-MM-DD]` — Extraction run. No new entries. Corpus unchanged at [total] beats.

**If extraction failed at any step:**
`[YYYY-MM-DD]` — Extraction run failed at Step [N]. Reason: [error]. No changes made to corpus.

---

## Failure handling

**Any doc fetch fails (Step 1):** stop immediately. Do not extract without the rules. Log to Notion: *Extraction aborted — could not read [file] from GitHub.*

**Corpus fetch fails (Step 2):** stop. Cannot determine last processed entry safely. Log to Notion.

**Notion read fails (Step 3):** stop. Cannot extract without source data. Log to Notion.

**GitHub commit fails (Step 6):** stop. Do not retry. Log error and details to Notion. Corpus is unchanged.

**Partial extraction (some entries produce beats, some do not):** commit what was extracted. Log both successes and empty entries in the Notion log.

---

## Output format reference

```json
[
  {
    "beat_id": "beat_042",
    "schema_version": "v3",
    "entry_ref": "Entry 20",
    "date": "2026-06-26",
    "emotion": "cautious excitement",
    "emotion_valence": 0.5,
    "emotion_arousal": 0.4,
    "pain_gain": "gain",
    "activity_type": "building",
    "action": "Built a new extraction skill and tested it end to end for the first time.",
    "verbatim": "It actually worked. Like, it just worked.",
    "job_to_be_done": "Close the loop between voice note and structured corpus automatically.",
    "complexity": 3,
    "subject": "self",
    "open_question": null,
    "phase": null,
    "themes": ["#builder-identity", "#delegation", "#build-surface-constraints"]
  }
]
```

---

*Created by Charline x Claude — June 26, 2026 — v3.1*
