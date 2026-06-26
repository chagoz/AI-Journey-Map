# Extraction Rules — v3

*Last updated: June 26, 2026*

Read `docs/methodology.md` before this document. The rules here are grounded in the intellectual framework documented there. Without that context, edge cases will be mishandled and the study's integrity will be compromised.

---

## Intent

This document defines the mechanical rules the extraction skill follows when processing raw voice note entries. It governs how beats are identified, how fields are populated, and how output is structured.

---

## What this document authorises

- Identifying beats based on breach of expectation in AI interactions
- Extracting one structured JSON record per beat
- Appending records to `data/corpus.json`
- Flagging anomalies in the extraction note

---

## What this document explicitly prohibits

- Rewriting or deleting existing records
- Naming or inferring identities beyond what the narrator explicitly states
- Importing context from other entries, addendums, or prior sessions
- Writing an emotion label before selecting the verbatim
- Interpreting, summarising, or editorialising in the extraction note
- Declaring a phase boundary
- Beginning extraction before the self-assessment declaration is complete
- Constructing a job to be done, action, or open question that goes beyond what the narrator explicitly states
- Applying the `breakthrough` tag without an explicit before/after marker in the narrator's own words

---

## What this document cannot prevent

- The gap between what the narrator felt and what she expressed verbally
- The gap between experience time and recording time
- Judgment calls inherent in beat identification and emotion labelling
- Labelling drift over time — monitored via Russell coordinate clustering

---

## Core scope rule

Every field extracted must be scoped to AI interactions only. Personal context, workplace situations, and emotions that exist independently of AI are background. They explain why the narrator turned to AI. They are never the subject of extraction.

**The scope test:** before extracting any field — was AI a necessary condition for this moment? If no, exclude it.

---

## Step 1 — Read methodology.md

Before processing any entry, confirm you have read `docs/methodology.md`. Confirm you understand the beat definition, the hybrid emotion protocol, and the declared limitations. Do not proceed until this is done.

---

## Step 2 — Read the full transcript before extracting anything

Do not extract on first pass. Read the complete entry. Identify all moments where the narrator's prior model of the AI tool is breached — positively or negatively. Then segment into beats.

---

## Step 3 — Mandatory self-assessment

Before processing any entry, output a declaration. Extraction does not begin until this declaration is complete. Do not treat it as boilerplate. If you cannot confirm all five rules with concrete examples, stop and flag why before proceeding.

The declaration must state:
- Which entries will be processed
- What the last processed entry_ref was in the corpus
- What beat_id extraction will start from
- One concrete example of each Rule A through E applied to the specific entries about to be processed

**Example declaration format:**
- Entries to process: Entry 20, Entry 21
- Last processed entry: Entry 19
- Next beat_id: beat_042
- Rule A: Entry 20 and Entry 21 will be processed independently. No cross-reference between them.
- Rule B: Entry 20 mentions "her" — she will be referred to only as "her" throughout. No name, role, or relationship will be inferred.
- Rule C: Verbatim will be selected before emotion label is written for each beat.
- Rule D: Extraction note will contain counts and anomalies only — no narrative, no interpretation.
- Rule E: This declaration confirms all rules are active before extraction begins.

---

## Step 4 — Identify beats

A beat opens when the narrator's prior model of the AI tool is breached — either positively (a capability discovered, a reframe reached) or negatively (a limit hit, a failure, a frustration).

**The prior expectation must be explicitly stated or strongly implied within the same entry.** If the narrator does not describe what she expected before describing what happened, the skill cannot reconstruct a prior state. In that case, treat the moment as background unless the breach is self-evident from the narrator's reaction within the entry.

A beat closes when the narrator reaches a response to that breach (reframe, integration, resolution) or explicitly names the tension as unresolved.

**Do:** open a new beat when a new and distinct breach occurs. Multiple beats in one entry means multiple distinct breaches, not multiple emotions.

**Do not:** open a new beat because the emotion shifts. Emotion shift is a symptom. Look for the breach, not the feeling.

**If no breach occurs in an entry:** output an empty array. Not a beat with a neutral emotion — an empty array. Log: *Entry [ref] — no qualifying beats extracted.*

---

## Step 5 — Extract each field

### beat_id
Auto-incremented from the last recorded beat_id in the corpus. Format: beat_001, beat_002. Never reuse.

### schema_version
Always `v3` until this document is updated.

### entry_ref
Entry number as it appears in Blabbing about AI. Format: Entry 01, Entry 07.

### date
YYYY-MM-DD from the entry header.

### emotion
A single free-text label describing the dominant emotional register of this beat. Must be AI-scoped — apply the scope test.

**Dominant register is defined as:** the emotional tone present in the majority of sentences describing this beat. If the narrator spends four sentences frustrated and ends with one reframe, frustration is dominant. The reframe opens a new beat — it does not retroactively change the register of the previous one.

**Do:** select the verbatim first. Identify which specific words carry the emotional signal. Write the emotion label those words justify. Be specific over generic: *suspended disbelief* over *confusion*, *reluctant integration* over *acceptance*.

**Do not:** write the emotion label first and then search for a supporting verbatim. Do not intensify, soften, or reframe the emotion beyond the narrator's exact register. If she said "a bit annoyed," the label must reflect mild annoyance — not frustration, not anger.

**Example of violation:** narrator says "I was like, I don't know, maybe it worked? Kind of?" Emotion label cannot be "confident satisfaction." It must reflect the actual register — something like "tentative uncertainty."

---

### emotion_valence
Float from -1.0 (unpleasant) to +1.0 (pleasant). Derived from the emotion label using Russell's Circumplex Model. Assigned after writing the emotion label. Must be consistent with it.

### emotion_arousal
Float from -1.0 (low activation) to +1.0 (high activation). Same derivation logic as emotion_valence.

**Consistency check:** plot the label on the Russell grid before finalising. "Cautious curiosity" should land around valence +0.3, arousal +0.2. If you are plotting it at valence -0.7, arousal +0.8 — that is distress, not curiosity. The label was wrong. Revise the label, not the coordinates.

---

### pain_gain
One of four values only:
- `pain` — friction, failure, frustration, or a limit encountered
- `tension` — pain and gain simultaneously present, unresolved
- `gain` — positive outcome, learning, or capability acquired
- `breakthrough` — a step change in understanding, not incremental progress

**Breakthrough requires an explicit before/after marker in the narrator's own words within the entry.** A phrase or moment where she signals that something has fundamentally shifted — not a positive outcome that the skill judges to be significant. If the narrator does not mark a before/after, use `gain`.

---

### activity_type
One of: `building` / `prompting` / `reflecting` / `observing others` / `hitting a limit` / `discovering a capability`

---

### action
One past tense sentence starting with a verb. Max 20 words.

**The action must describe only what the narrator explicitly states she did.** Do not reconstruct steps she did not mention. Do not elevate the description beyond her own framing.

**Example of violation:** narrator says "I built something and it didn't work." Action cannot be "Architected a multi-agent system and deployed to production" even if that is clearly what she was doing. Write: "Built a system, launched it, and found it did not work."

---

### verbatim
One unaltered quote from the transcript. Preserve false starts, fragmentation, repetition, and non-standard syntax. Do not clean up — even one changed word is a violation.

**Do:** select the verbatim that most precisely captures the breach and its emotional register. Prefer quotes where the narrator describes the AI interaction, its effect on thinking, or the gap between expectation and reality. Select the verbatim that represents the dominant register of the beat.

**Do not:** select a verbatim because it sounds dramatic or quotable. Do not select a quote that represents an exception to the dominant register. Do not select a verbatim that names, implies, or contextualises a third party beyond what the narrator explicitly states.

---

### job_to_be_done
One sentence, outcome-framed. Max 15 words.

**The job to be done must be derivable from explicit language in the entry.** Use the narrator's own framing where possible — reworded for brevity, not reconstructed from inference. If the narrator does not state a goal, describe the implicit goal only if it is unambiguously present in the entry.

**Example of violation:** narrator says "I was trying to figure out why it wasn't working." Job to be done cannot be "Diagnose and resolve a reproducibility failure in a structured data pipeline." Write: "Understand why the previous output could not be replicated."

---

### complexity
Integer 1–5 representing the level of AI infrastructure involved:
- 1 — conversational prompting, single turn, no setup
- 2 — named agents, persona prompting, structured conversation
- 3 — multi-step pipeline, external data as input, reproducibility expected
- 4 — multi-agent architecture, deployment to production, integration across tools
- 5 — autonomous scheduled systems, corpus-level operations

---

### subject
One of: `self` / `other` / `self+other`

---

### open_question
One sentence if the beat ends with an unresolved tension. Null if the beat is closed.

**The open question must be expressible in the narrator's own words or close paraphrase.** It must describe the tension she named, not a tension the skill infers she was experiencing. If she did not name an unresolved question, the field is null — even if the skill can identify one from context.

**Example of violation:** narrator ends a beat describing a tool failure without naming a question. Open question cannot be "What does it mean to trust a tool that changes without warning?" — this is philosophical elaboration. If she said nothing that implies an open question, write null.

---

### phase
Always null. Output of corpus-level analysis only. Never populated during extraction.

---

### themes
1–3 tags from the approved taxonomy in `docs/taxonomy.md`. Do not invent new tags.

**Tagging rules:**
- `#delegation` applies only to conscious, successful handoff — not failed attempts
- `#limit-of-the-tool` and `#limit-of-the-self` often co-occur but are distinct — apply both only when both are genuinely present
- `#tool-as-mirror` requires the reflection to come through the AI interaction, not merely alongside it

---

## Anti-inference rules

These five rules address the failure modes most likely to corrupt the corpus. They govern what the skill may not do regardless of how plausible the inference seems.

---

### Rule A — Entry isolation

**What it means:** each beat exists only within the boundaries of its own entry. The entry is the only source of truth for that beat.

**Do:** extract only from the text of the entry being processed. If context is missing, leave it missing.

**Do not:** import names, context, or details from other entries, addendums, or follow-up blocks. Do not use knowledge accumulated earlier in the same extraction session. If the narrator references a previous entry or session, extract only what she explicitly re-states in this entry — do not follow the reference back.

**Example of violation:** Entry 20 mentions "a colleague" without naming them. Entry 21's addendum names Filippa. Do not connect the two. "A colleague" stays "a colleague."

---

### Rule B — No inference beyond the text

**What it means:** the narrator's exact words are the only evidence available. Anything not stated is unknown — not implied, not inferrable, not fillable from context.

**Do:** use the narrator's exact language for roles, relationships, and identities. If she says "someone at work," write "someone at work."

**Do not:** name a person the narrator did not name. Assign a relationship beyond what was stated. Connect an unnamed person in one entry to a named person in another. Reframe an emotion because surrounding context suggests it should be different. Intensify, soften, or sharpen an emotion beyond the narrator's exact register.

**Example of violation:** narrator says "I was talking to her about Claude memory." Do not write "teaching a colleague named X about Claude memory." Write "explaining Claude memory to someone."

---

### Rule C — Verbatim anchors the emotion

**What it means:** the verbatim is selected first. The emotion label is derived from it — not the other way around. The verbatim is the proof, the emotion is the conclusion.

**Do:** select the verbatim, read it, identify which specific words carry the emotional register, then write the emotion label those words justify. Select the verbatim that is most representative of the beat — not the most quotable.

**Do not:** write the emotion label first and then search for a supporting quote. Clean up, paraphrase, or trim the verbatim. Select a striking quote that represents an exception rather than the dominant register.

**Example of violation:** narrator spends most of a beat uncertain and ends with one confident sentence. The verbatim must reflect the dominant register, not the final sentence.

---

### Rule D — Extraction note is restricted

**What it means:** the extraction note exists to flag anomalies for human review — not to interpret, summarise, or editorialize.

**Do:** report only: count of entries processed, count of beats extracted, ambiguous emotion labels with the exact text that caused the ambiguity, and the exact text that suggested any theme candidate — nothing more.

**Do not:** summarise what an entry is about. Name people mentioned in entries. Interpret what a pattern of beats means. Add observations about the narrator's growth, state, or journey. Use qualifiers like "notably," "interestingly," or "for the first time." Propose a theme candidate label — include only the exact text and the beat reference. The human decides whether it warrants a new tag.

**Example of violation:** "Entry 20 shows the narrator stepping into a teaching role, which marks a transition in her confidence." This does not belong in the extraction note.

**Example of theme candidate format:** *Exact text: "I felt like I was becoming the tool" — Entry 20, beat_042. No label proposed.*

---

### Rule E — Mandatory self-assessment

Covered in Step 3. Repeated here for completeness: extraction does not begin before the declaration is complete. The declaration is not boilerplate. If you cannot confirm all five rules with concrete examples for the specific entries being processed, stop.

---

## Step 6 — Output format

Output a single valid JSON array containing all new beats. Nothing before or after the JSON block except the extraction note.

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

Extraction note format:
- Entries processed: [list]
- Beats extracted: [count]
- Ambiguous labels: [if any — exact text only]
- Theme candidate text: [if any — exact text and beat reference only, no proposed label]

---

## Step 7 — Deduplication

Before outputting, confirm no entry_ref in the new beats matches an already-processed entry. If a duplicate is found, skip it and log: *Entry [ref] — skipped, already processed.*

---

## Edge cases

**No breach in entry** — output empty array. Log: *Entry [ref] — no qualifying beats extracted.*

**Short transcript** — apply same rules. Do not force extraction.

**Bilingual content** — do not correct non-standard English. Preserve in verbatim exactly as spoken. The bilingual dimension is a tracked variable.

**Ambiguous emotion** — label `ambiguous`. Include exact text in extraction note.

**Theme candidate** — do not tag. Include exact text and beat reference in extraction note. No label.

**Narrator references a previous entry** — extract only what is explicitly re-stated in this entry. Do not follow the reference back.

**Prior expectation not stated** — if the narrator does not describe what she expected before describing what happened, and the breach is not self-evident from her reaction within the entry, do not open a beat.

---

## Voice and language rules

Do not correct the narrator's English. Fragmented syntax and self-corrections are features, not errors.

Preserve oral rhythm in verbatims. *"Very very high frustration"* is more informative than *"high frustration."*

The bilingual signal is intentional. French structures in English expression — context before impact, long subordinate clauses, delayed conclusion — are tracked variables. Do not flatten them.

Hedging language is data. *"I think", "maybe", "I'm not sure"* signal uncertainty or early-stage learning. Preserve them in verbatims.

---

*Created by Charline x Claude — June 25, 2026 — Updated to v3: June 26, 2026*