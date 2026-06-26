# Schema Reference — v3

*Last updated: June 26, 2026*

This document defines the structure of one record in `data/corpus.json`. Read `docs/methodology.md` for the intellectual foundation and `docs/extraction-rules.md` for the rules governing how each field is populated. Schema.md describes what each field is. Those documents define how to fill it correctly.

One record = one beat. A beat is a unit of experience bounded by a breach of expectation in an AI interaction. It opens when the narrator's prior model of the tool is violated. It closes when she reaches a response to that breach or explicitly names the tension as unresolved. See methodology.md for the full operational definition.

---

| field | type | description |
|-------|------|-------------|
| `beat_id` | string | Unique identifier. Auto-incremented. Format: beat_001, beat_002. Never reused. |
| `schema_version` | string | Extraction rules version that produced this record. Format: v3. |
| `entry_ref` | string | Parent voice note. Format: Entry 01, Entry 07. |
| `date` | string | Date of the voice note. Format: YYYY-MM-DD. |
| `emotion` | string | Dominant emotional register of the beat. AI-scoped only — apply the scope test. Free label. Derived from the verbatim, not from overall impression. See extraction-rules.md Rule C. |
| `emotion_valence` | float | Valence coordinate on Russell's Circumplex Model. Range: -1.0 (unpleasant) to +1.0 (pleasant). Must be consistent with the emotion label. |
| `emotion_arousal` | float | Arousal coordinate on Russell's Circumplex Model. Range: -1.0 (low activation) to +1.0 (high activation). Must be consistent with the emotion label. |
| `pain_gain` | enum | `pain` / `tension` / `gain` / `breakthrough`. Breakthrough requires an explicit before/after marker in the narrator's own words. |
| `activity_type` | enum | `building` / `prompting` / `reflecting` / `observing others` / `hitting a limit` / `discovering a capability` |
| `action` | string | One past tense sentence starting with a verb. Max 20 words. Describes only what the narrator explicitly states she did — not reconstructed from inference. |
| `verbatim` | string | One unaltered quote from the transcript. Preserves false starts, fragmentation, and repetition. Selected to represent the dominant register of the beat — not for drama or quotability. |
| `job_to_be_done` | string | What the narrator explicitly states she was trying to accomplish. One sentence, max 15 words. Uses narrator's own framing where possible. |
| `complexity` | integer | 1–5. Level of AI infrastructure involved. See extraction-rules.md for scale definitions. |
| `subject` | enum | `self` / `other` / `self+other` |
| `open_question` | string or null | The unresolved tension the narrator named at the end of the beat, in her own words or close paraphrase. Null if the beat is closed or if she named no tension. Never inferred. |
| `phase` | null | Always null. Output of corpus-level analysis only. Never populated during extraction. |
| `themes` | array | 1–3 tags from the approved taxonomy. See taxonomy.md. Maximum 3. |

---

*Schema v3 — added emotion_valence and emotion_arousal. Updated beat definition to breach-based. Tightened field descriptions to reflect anti-inference rules. June 26, 2026.*