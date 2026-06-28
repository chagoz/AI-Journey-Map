## 2026-06-28
2026-06-28 — Retroactive enrichment: emotion_valence and emotion_arousal added to beat_001 through beat_041. Derived from existing emotion labels and verbatims using Russell Circumplex Model. No other fields modified. Schema enrichment only — no extracted values changed.

# Changelog

*AI Journey Map â all rule changes, schema versions, and taxonomy updates. Most recent first.*

---

## 2026-06-26

**Schema v3**
- Added `emotion_valence` field â float -1.0 to +1.0, Russell Circumplex valence axis
- Added `emotion_arousal` field â float -1.0 to +1.0, Russell Circumplex arousal axis
- Updated beat definition from emotion-shift based to breach-based (Bruner/Burke)
- Tightened all field descriptions to reflect anti-inference rules
- Total fields: 17

**Extraction rules v3**
- Added intent, authorises, prohibits, and cannot-prevent sections at document opening
- Added breach-based beat identification replacing emotion-shift logic
- Added five anti-inference rules (A through E) with do/do not/example structure
- Added gap-filling clauses: dominant register definition, prior expectation constraint, job-to-be-done grounding, action grounding, breakthrough marker requirement, open question grounding, extraction note exact-text-only rule
- Added mandatory self-assessment declaration with concrete examples per rule
- Added pointer to methodology.md at document opening
- Schema version updated to v3 throughout

**Methodology v1 â new document**
- Reflexivity statement: declared biases, bilingual variable, prior disposition
- Beat definition grounded in Bruner (1986, 1991) and Burke (1945) â canonicity and breach, dual landscape
- Emotion labelling hybrid protocol: free labels anchored by verbatim, Russell grid as validation layer
- Rejection of fixed taxonomies: Ekman (too coarse), Plutchik (wrong domain), LIWC (wrong granularity)
- Pennebaker borrowed as principle not as categories
- Declared limitations: unexpressed emotion, performed vs felt, experience-to-recording gap, model bias, phase boundary prohibition
- Full references section

**Taxonomy v2**
- Full definitions added to all 13 tags
- Theoretical anchor added: Silverstone domestication theory (1992, 1994), four phases mapped to tag clusters
- Application rules, linguistic anchors, and do/do not pairs added per tag
- Emergent theme graduation threshold defined: 15% of total beats triggers review
- `#reframe` tightened: requires explicit before/after marker in narrator's language
- `#dependency` tightened: requires narrator to name the reliance, not inferred from usage
- `#tool-as-mirror` tightened: tool must be causally connected to the reflection

**Extraction skill v3.1**
- Fully cloud-based: reads all docs and corpus from GitHub raw URLs and API
- No local filesystem dependency
- GitHub API write: direct PUT to corpus.json, no local script required
- Credentials stored in Cowork project instructions, never in files
- Added schema.md as Step 1 document (4 docs total before extraction)
- Added Notion project log update as final step after each run
- Failure handling: stops and logs to Notion at any failure point, never partial commits

**README updated**
- Full rewrite for main repo: research framing, reflexivity statement, methodology summary, repository structure
- Template repo README: fork-oriented, methodology-first, no personal data

---

## 2026-06-25

**Schema v2**
- Added `beat_id` field â unique identifier, auto-incremented, format beat_001
- Added `schema_version` field â tracks which extraction rules version produced each record
- Decision: corpus is append-only. No reprocessing of existing records.

**Extraction rules v1**
- Initial document. Scope rule, beat identification, all field definitions, output format, deduplication, edge cases, voice and language rules.

**Taxonomy v1**
- 8 core themes defined: `#tool-as-mirror` `#limit-of-the-tool` `#limit-of-the-self` `#dependency` `#delegation` `#reframe` `#observation-of-others` `#language-and-expression`
- 5 emergent themes defined: `#builder-identity` `#ai-policy-friction` `#mobile-and-mobility` `#bilingual-cognition` `#build-surface-constraints`
- `#build-surface-constraints` added after Entry 07 extraction test

**Corpus v1 â first extraction**
- 41 beats extracted across 19 entries (May 30 to June 25, 2026)
- All records tagged schema_version v2
- Retroactive extraction: all entries processed manually in one pass

**Key architecture decisions**
- Raw data source: Notion, Blabbing about AI. Single source of truth, untouched after recording.
- Processed corpus: GitHub JSON, append-only, one record per beat
- Trigger: daily scheduled task at 09:00 via Cowork
- Frontend: Lovable (React). Two views planned: journey map and galaxy
- Phase detection: future layer, runs at corpus volume, output never input
- Scale threshold: revisit database architecture at 300 beats (~12-18 months at current pace)
- Forkability: template repo with anonymised sample beats and full methodology docs

---

*Created by Charline x Claude â June 25, 2026 â Updated June 26, 2026*
