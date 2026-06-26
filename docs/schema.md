# Schema Reference — v2

*Last updated: June 25, 2026*

One record = one emotional beat. A beat is a discrete moment where an AI interaction triggered a distinct emotional or intellectual response.

---

| field | type | description |
|-------|------|-------------|
| `beat_id` | string | Unique identifier. Format: beat_001, beat_002… Auto-incremented. Never reused. |
| `schema_version` | string | Which extraction rules version produced this record. Format: v1, v2… |
| `entry_ref` | string | Parent voice note. Format: Entry 01, Entry 07… |
| `date` | string | Date of the voice note. Format: YYYY-MM-DD. |
| `emotion` | string | Dominant emotional register, AI-scoped only. Free label, specific over generic. |
| `pain_gain` | enum | `pain` / `tension` / `gain` / `breakthrough` |
| `activity_type` | enum | `building` / `prompting` / `reflecting` / `observing others` / `hitting a limit` / `discovering a capability` |
| `action` | string | One implied sentence in past tense. Starts with a verb. Max 20 words. |
| `verbatim` | string | One unaltered quote from the transcript. Preserves false starts and fragmentation. |
| `job_to_be_done` | string | What the narrator was trying to accomplish. One sentence, max 15 words. |
| `complexity` | integer | 1–5. Infrastructure dependency scale. See extraction rules for definitions. |
| `subject` | enum | `self` / `other` / `self+other` |
| `open_question` | string or null | Unresolved tension at end of beat. Null if beat is closed. |
| `phase` | null | Always null until corpus-level analysis earns it. Output, never input. |
| `themes` | array | 1–3 tags from approved taxonomy. See taxonomy.md. |

---

*Schema v2 — added beat_id and schema_version over v1.*
