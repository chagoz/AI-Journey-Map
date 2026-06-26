# Extraction Skill — Rules & Schema v2

*Last updated: June 25, 2026*

This document defines the rules the extraction skill follows when processing a raw voice note entry. It is the single source of truth for extraction logic. Any change to these rules must be versioned and logged in changelog.md.

---

## Purpose

Read a raw voice note transcript, identify distinct emotional beats triggered by AI interactions, and output one structured JSON record per beat. Records are appended to data/corpus.json. Existing records are never rewritten.

---

## Core rule — scope

Every field extracted must be scoped to AI interactions only.

Personal context, workplace situations, and emotions that exist independently of AI are background. They explain why the narrator turned to AI. They are never the subject of extraction.

**The scope test:** before extracting any emotion, action, or verbatim — was AI a necessary condition for this moment? If no, exclude it.

---

## Step 1 — Read the full transcript before extracting anything

Do not extract on first pass. Read the complete transcript, identify all AI interaction moments, then segment into beats. A beat is a discrete moment with a distinct AI-triggered emotional register.

---

## Step 2 — Identify beats

A new beat begins when:
- The emotion shifts detectably
- A new AI interaction begins (different tool, different task, different session)
- The narrator explicitly marks a transition

Minimum one beat per entry. Do not fragment a single continuous emotional moment into multiple beats for granularity's sake.

---

## Step 3 — Extract each field

**beat_id** — Auto-incremented from last recorded beat_id in corpus. Format: beat_001.

**schema_version** — Always `v2` until this document is updated.

**entry_ref** — Entry number as it appears in source. Format: Entry 01.

**date** — YYYY-MM-DD.

**emotion** — Single label, AI-scoped. Specific over generic: *suspended disbelief* over *confusion*. Do not force positive framing.

**pain_gain** — `pain` / `tension` / `gain` / `breakthrough`. Breakthrough = step change, not incremental.

**activity_type** — `building` / `prompting` / `reflecting` / `observing others` / `hitting a limit` / `discovering a capability`

**action** — One past tense sentence starting with a verb. Max 20 words.

**verbatim** — One unaltered quote. Preserve false starts and fragmentation. Prefer quotes where the narrator describes the AI interaction, its effect on thinking, or the gap between expectation and reality.

**job_to_be_done** — One sentence, outcome-framed. Max 15 words.

**complexity** — 1: conversational prompting / 2: named agents / 3: multi-step pipeline with external data / 4: multi-agent architecture, deployment / 5: autonomous scheduled systems

**subject** — `self` / `other` / `self+other`

**open_question** — One sentence if beat ends unresolved. Null if beat is closed. Most likely on pain/tension beats.

**phase** — Always null. Output of corpus-level analysis only.

**themes** — 1–3 tags from taxonomy. Do not invent new tags — flag candidates in extraction notes instead.

---

## Step 4 — Output format

```json
{
  "beat_id": "beat_001",
  "schema_version": "v2",
  "entry_ref": "Entry 01",
  "date": "2026-05-30",
  "emotion": "curiosity shading into satisfaction",
  "pain_gain": "gain",
  "activity_type": "reflecting",
  "action": "Recognised that a custom agent had surfaced an invisible communication pattern.",
  "verbatim": "There is something in me that is always about bringing the context before talking about impact — and I needed to reverse that.",
  "job_to_be_done": "Use AI as a mirror to surface invisible communication habits.",
  "complexity": 2,
  "subject": "self",
  "open_question": null,
  "phase": null,
  "themes": ["#tool-as-mirror", "#language-and-expression", "#bilingual-cognition"]
}
```

---

## Step 5 — Deduplication

Before outputting, confirm entry_ref has not already been processed. If it has, skip and log: *Entry [ref] — skipped, already processed.*

---

## Edge cases

**No AI-triggered moments** — Output empty array. Log: *Entry [ref] — no qualifying beats extracted.*

**Short transcript** — Apply same rules. Do not force extraction.

**Bilingual content** — Do not correct non-standard English. Preserve in verbatim exactly as spoken.

**Ambiguous emotion** — Label `ambiguous`. Add note in open_question.

**New theme candidate** — Do not tag. Add note: *Theme candidate: [tag] — observed in [entry_ref], beat [beat_id].*

---

## Voice and language rules

Do not correct the narrator's English. Fragmented syntax and self-corrections are features, not errors.

Preserve oral rhythm in verbatims. *"Very very high frustration"* is more informative than *"high frustration."*

The bilingual signal is intentional. French structures in English expression are tracked variables.

Hedging language is data. *"I think", "maybe", "I'm not sure"* signal uncertainty or early-stage learning. Preserve them.

---

*Created by Charline x Claude — June 25, 2026 — v1.0*
