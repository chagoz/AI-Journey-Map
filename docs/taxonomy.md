# Theme Taxonomy — v3

*Last updated: September 25, 2026*

This document defines the approved theme tags for the AI Journey Map corpus. It is read by the extraction skill alongside each tagging decision. Each tag definition is designed to be fetched as context at the moment of application.

Read `docs/methodology.md` for the intellectual foundation. Read `docs/extraction-rules.md` for the general tagging rules. This document governs what each tag means and when to apply it.

---

## Tagging constraints

- Maximum 3 themes per beat
- Do not invent new tags — flag candidates in the extraction note with exact text only
- Tags are applied to what is explicitly present in the entry, not to what is inferred
- When two tags seem equally applicable, choose the one most directly anchored in the verbatim

---

## Theoretical anchor

The theme taxonomy is oriented around Roger Silverstone's domestication theory (1992, 1994), which describes how individuals incorporate new technologies into their lives and practices. Silverstone identified four phases: appropriation (taking ownership), objectification (giving the technology a place), incorporation (integrating it into routines), and conversion (using it to signal something to the outside world).

The taxonomy does not enforce these phases as rigid categories. It uses them as orientation: a loose map of the territory the tags are collectively trying to cover. Tags that track the psychological dimension of adoption — what the tool reflects back, where the limits are, how meaning is made — draw additionally on Pennebaker's linguistic approach to psychological state detection.

The taxonomy was built inductively from the first 19 entries of the corpus. It is designed to remain open. New tags emerge from the data, not from the framework.

Version 3 extends it from a full scan of 40 entries. Candidate text was surfaced by the extraction model, reviewed for internal coherence and external distinctness, and named by the author. A new tag must appear in at least 3 entries. Tags stay flat: parent themes will be derived later from real tag co-occurrence across the corpus, and will live in this document only, as a lookup.

**Loose mapping of tags to domestication phases:**

| Phase | Associated tags |
|-------|----------------|
| Appropriation — taking ownership | `#delegation` `#builder-identity` `#tool-as-mirror` `#trust-in-the-tool` `#how-i-learn` |
| Objectification — giving it a place | `#build-surface-constraints` `#limit-of-the-tool` `#governing-agents` `#cost-of-access` |
| Incorporation — integrating into routines | `#dependency` `#limit-of-the-self` `#mobile-and-mobility` `#cost-of-speed` `#interest-in-the-work` |
| Conversion — signalling to the outside world | `#observation-of-others` `#ai-policy-friction` `#value-visibility` `#collaborative-transparency` |
| Cross-phase | `#reframe` `#language-and-expression` `#bilingual-cognition` |

---

## Core themes

These tags are expected to recur throughout the corpus and will anchor the main clusters in the galaxy view. They have sufficient density to produce meaningful patterns at scale.

---

### #tool-as-mirror

**Definition:** a moment where the AI interaction reflects something back about the narrator's own thinking, communication patterns, or identity — something she could not have seen without the tool as mediator.

**Application rule:** the reflection must come through the AI interaction, not merely alongside it. The tool must be a necessary condition for the insight.

**Linguistic anchor:** look for language where the narrator describes discovering something about herself through what the tool produced, challenged, or named. Phrases like "I realised," "it showed me," "I hadn't seen that before" — when directly connected to an AI output.

**Do:** apply when the AI output is the mirror — when the narrator's self-knowledge is changed by what the tool surfaced.

**Do not:** apply when the narrator is simply using AI and happens to reflect on herself in the same entry. The tool must be causally connected to the reflection.

---

### #limit-of-the-tool

**Definition:** a moment where the narrator encounters a ceiling in what the AI tool can do — a capability gap, a reliability failure, or a structural constraint of the technology itself.

**Application rule:** the limit must be attributed to the tool, not to the narrator's knowledge or setup. If the narrator is uncertain whether the failure is hers or the tool's, apply `#limit-of-the-self` alongside or instead.

**Linguistic anchor:** look for language that attributes the failure or gap to the tool's behaviour. "It couldn't," "it didn't," "the tool just," "I expected it to but it."

**Do:** apply when the breach is in the tool's capability as the narrator experiences it.

**Do not:** apply when the narrator attributes the gap to her own prompting, knowledge, or setup.

---

### #limit-of-the-self

**Definition:** a moment where the narrator recognises that the tool can only go as far as her own knowledge, clarity of intent, or skill allows — the ceiling is in her, not in the tool.

**Application rule:** distinct from `#limit-of-the-tool`. The narrator attributes the constraint to herself. Both tags can co-occur when attribution is explicitly uncertain — but only when the narrator names the uncertainty herself.

**Linguistic anchor:** look for language of self-attribution. "I didn't know enough," "I couldn't formulate it," "it's on my side," "I realised I needed to know more before I could ask."

**Do:** apply when the narrator names her own knowledge or skill as the constraint.

**Do not:** apply when the skill infers this from context. The narrator must name it.

---

### #dependency

**Definition:** a moment where the narrator notices — consciously or with some unease — that the tool has become load-bearing in her thinking or workflow. Not habitual use, but noticed reliance.

**Application rule:** dependency requires the narrator to explicitly notice or name the reliance — not just use the tool heavily. Habitual use without commentary does not qualify.

**Linguistic anchor:** look for language of noticing or questioning the reliance. "I couldn't work without it," "I realised I was blocked," "how did I end up here," "I depend on it now." The noticing is the signal.

**Do:** apply when the narrator marks the reliance as something worth commenting on.

**Do not:** apply when the narrator simply uses the tool frequently without naming the dependency. Do not infer dependency from usage intensity.

---

### #delegation

**Definition:** a moment where the narrator consciously and successfully hands a task or decision to the AI — choosing to trust the tool with something she could have done herself.

**Application rule:** delegation requires conscious intent and at least partial success. Failed attempts to delegate do not qualify — those are `#limit-of-the-tool` or `#limit-of-the-self`.

**Linguistic anchor:** look for language of intentional handoff. "I asked it to," "I let it handle," "I gave it," "I trusted it with." The consciousness of the choice is the signal.

**Do:** apply when the narrator explicitly describes choosing to hand something to the tool and the handoff worked.

**Do not:** apply to failed delegations. Do not apply when the narrator uses AI without commentary on the choice to do so.

---

### #reframe

**Definition:** a moment where a frustration, failure, or limit is explicitly converted into a principle, insight, or new understanding by the narrator — within the same entry.

**Application rule:** the reframe must be explicit in the narrator's language within the entry. The skill cannot infer that a positive ending to a negative beat constitutes a reframe. The narrator must mark the shift herself.

**Linguistic anchor:** look for language that explicitly names a shift in understanding. "I realised," "what this taught me," "actually this means," "I now see it differently," "it goes back to" — when connected to a prior frustration or failure in the same beat.

**Do:** apply when the narrator explicitly names a new understanding derived from a negative experience.

**Do not:** apply when a beat ends positively after starting negatively without the narrator naming the shift. Do not infer reframe from emotional arc alone.

---

### #observation-of-others

**Definition:** a moment where the narrator describes watching or hearing how other people relate to AI — their adoption posture, their use patterns, their resistance or enthusiasm.

**Application rule:** the subject of the beat is someone other than the narrator. The narrator is the observer, not the actor.

**Linguistic anchor:** look for third-person description of AI use or attitude. "She was using it to," "he said," "they don't know," "I watched someone."

**Do:** apply when the primary subject of the beat is another person's relationship with AI.

**Do not:** apply when the narrator mentions others briefly but remains the primary subject of the beat.

---

### #language-and-expression

**Definition:** a moment where how the narrator speaks or writes becomes the subject — where language itself is examined, challenged, or changed by the AI interaction.

**Application rule:** the focus must be on language as a medium, not on content. This tag tracks moments where the narrator notices something about her own expression — in English, in French, or in the bilingual space between them.

**Linguistic anchor:** look for language about language. References to word choice, sentence structure, communication patterns, the act of writing or speaking, the gap between what she meant and what she said.

**Do:** apply when the AI interaction surfaces something about the narrator's own language or expression.

**Do not:** apply when the narrator is simply communicating through AI without the language itself becoming the subject.

---

## Emergent themes

These tags appeared in the first corpus pass. They may grow into core themes, remain niche, or disappear. Their density is tracked over time. A review is triggered when any emergent theme appears in more than 15% of all beats — at that point it is considered for promotion to core.

---

### #builder-identity

**Definition:** a moment where the narrator questions, discovers, or expands what it means to build and ship as a designer using AI — where professional identity is in motion, or where she questions which part of the work is hers and which belongs to the tool.

**Application rule:** the identity dimension must be explicit. The narrator must be commenting on what she is, not just what she is doing.

**Linguistic anchor:** look for language about self-definition. "I am a builder," "this is what I do," "I didn't know I could," "what does this make me," "roles don't matter anymore," "what's mine," "where do I sit versus it," "an AI operator."

**Do:** apply when the narrator explicitly comments on her identity as a builder or designer in relation to what AI enables.

**Do not:** apply when she is simply building something without commenting on what that means for her identity.

---

### #ai-policy-friction

**Definition:** a moment where institutional rules, permissions, or enterprise constraints shape or block AI adoption — the gap between what the narrator can do personally and what the organisation allows, including top-down organisational pushes for AI adoption, such as productivity targets or mandated tools.

**Application rule:** the friction must be institutional — rules, policies, IT constraints, enterprise configurations. Personal technical limitations belong to `#limit-of-the-self` or `#limit-of-the-tool`.

**Linguistic anchor:** look for language about organisational constraint. "The company," "I'm not allowed," "enterprise version," "the policy says," "I had to ask IT," "the CEO decided," "everyone should," "pushed via Slack."

**Do:** apply when the constraint comes from an institutional layer above the narrator's own capability.

**Do not:** apply to technical limitations that have nothing to do with organisational policy.

---

### #mobile-and-mobility

**Definition:** a moment where AI use happens outside a desk context — during commute, walking, outdoors — and where that mobility changes the nature of the interaction or output.

**Application rule:** the mobility must be relevant to the beat, not just incidental. If the narrator happens to be on a commute but the interaction is identical to a desk interaction, mobility is background.

**Linguistic anchor:** look for language that names the context as meaningful. "On my way," "walking," "in the car," "without a screen," "voice only."

**Do:** apply when the mobile context shapes or enables something in the AI interaction that would not have happened at a desk.

**Do not:** apply when mobility is mentioned but has no bearing on the beat.

---

### #bilingual-cognition

**Definition:** a moment where the gap between French cognitive structure and English expression becomes visible — where the narrator notices the bilingual dimension of her thinking or communication.

**Application rule:** the bilingual dimension must be explicitly noticed or named by the narrator, or be directly visible in the verbatim through structural features (context-before-impact, long subordinate clauses, delayed conclusion).

**Linguistic anchor:** look for explicit references to French/English difference, or for verbatim quotes that show the French cognitive pattern in English expression clearly enough to note.

**Do:** apply when the bilingual gap is a signal worth tracking — either named by the narrator or structurally evident in the verbatim.

**Do not:** apply to every entry simply because the narrator is French. The bilingual dimension must be present and relevant in this specific beat.

---

### #build-surface-constraints

**Definition:** a moment where the narrator encounters the specific frustration of the gap between using Claude as a product and building with Claude as a platform — where the tool's own capabilities become the ceiling of what she can create.

**Application rule:** this tag is specifically about the build surface — the gap between the native Claude experience and what can be constructed with skills, tools, or the API. It is not a general limit tag.

**Linguistic anchor:** look for language that names the gap between experience and construction. "What I can build," "native feels better," "the skill doesn't match," "Claude as a user versus Claude as a builder."

**Do:** apply when the narrator is explicitly comparing what Claude does as a product with what she can make it do as a builder.

**Do not:** apply to general AI limitations. This tag is specifically about the build surface gap.

---

### #value-visibility

**Definition:** a moment where the narrator considers how the value of her AI-enabled work is seen, recognised or understood by others: colleagues, the market, or the design profession.

**Application rule:** the audience must be explicit. The narrator is thinking about how her work or skills land with someone else, not about what the work is.

**Linguistic anchor:** "legitimate," "express them in stakeholder meetings," "my profile doesn't match the boxes," "package someone like me," "the role of design."

**Do:** apply when recognition, legibility or market fit of her AI practice is the subject.

**Do not:** apply when she reflects on her identity without an audience in view. That belongs to `#builder-identity`.

---

### #trust-in-the-tool

**Definition:** a moment where the narrator describes trust, or its absence, as a feeling toward the AI tool itself: being able to rely on it, expecting it to behave, feeling let down by it.

**Application rule:** trust must be expressed as a relational feeling. Checking whether an output is correct belongs to `#governing-agents`. Trust in the company behind the tool belongs to `#cost-of-access`.

**Linguistic anchor:** "trust," "in control," "I projected an expectation," "blindly trust the system," "weird to say that about a machine."

**Do:** apply when the narrator describes her felt relationship of reliance or disappointment with the tool.

**Do not:** apply to verification routines, audits or output errors without a relational dimension.

---

### #cost-of-speed

**Definition:** a moment where the pace AI enables takes a felt toll on the narrator's energy, time boundaries or personal space, or where she questions whether speed is a gain at all.

**Application rule:** the cost must be personal and experienced: exhaustion, overwork, lost space, speed that feels empty. Noticing reliance on the tool belongs to `#dependency`.

**Linguistic anchor:** "exhausted," "draining," "ate me alive," "not a healthy way of working," "I don't want to go faster," "is AI really accelerating anything."

**Do:** apply when speed, intensity or volume of AI-enabled work has a stated effect on her.

**Do not:** apply to money, limits or pricing. That belongs to `#cost-of-access`.

---

### #interest-in-the-work

**Definition:** a moment where the narrator reflects on her interest, creativity or sense of meaning in the work itself, as AI changes which tasks she does.

**Application rule:** the reflection must be about engagement with the work: what excites her, what bores her, what feels creative or empty.

**Linguistic anchor:** "boring," "not really creative," "losing interest," "positive juice," "what motivates me most," "the doing of it isn't where my value is."

**Do:** apply when AI's effect on what feels interesting or meaningful to her is explicit.

**Do not:** apply when she describes a task's efficiency without saying how it feels to do it.

---

### #cost-of-access

**Definition:** a moment where pricing, usage limits, licences or the vendor's business model shape the narrator's use of AI or her trust in the company providing it.

**Application rule:** the constraint or concern must come from the commercial layer: plans, credits, limits, upgrades, opt-ins. Institutional permissions belong to `#ai-policy-friction`.

**Linguistic anchor:** "limit," "credits," "Pro," "Max," "pay that much to do that little," "tricked," "dark pattern," "stickiness."

**Do:** apply when cost or commercial design is the subject, including trust in the vendor as a company.

**Do not:** apply to capability limits of the model. That belongs to `#limit-of-the-tool`.

---

### #how-i-learn

**Definition:** a moment where the narrator reflects on the way she learns, with or through AI: the method, the pace, the depth, or the practice of reflecting itself.

**Application rule:** the subject must be her own learning process, not a gap in her knowledge. Noticing what she does not know belongs to `#limit-of-the-self`. Others' learning belongs to `#observation-of-others`.

**Linguistic anchor:** "learn about the way I learn," "learning by experiencing," "debate with Claude," "good enough, not deep," "this daily reflection has been part of my improvement."

**Do:** apply when she describes how she acquires understanding.

**Do not:** apply to a single fact learned without reflection on the process.

---

### #collaborative-transparency

**Definition:** a moment where the narrator considers how AI work is shared, made visible or understood between people, or how AI may isolate people working on the same problem.

**Application rule:** the collaborative dimension must be explicit: others need to see, comment on, share or start from the same context.

**Linguistic anchor:** "transparency," "collaborative setting," "how can people comment on AI output," "keep all my skills to myself," "isolate us," "no standard."

**Do:** apply when the visibility or shareability of AI work between people is the subject.

**Do not:** apply to solo workflows with no mention of others.

---

### #governing-agents

**Definition:** a moment where the narrator writes rules for, audits, verifies or corrects AI agents, or notices drift from their mission.

**Application rule:** the act of governance must be present: defining rules, checking outputs against them, catching deviation. A conscious handoff of a task belongs to `#delegation`.

**Linguistic anchor:** "the rules of our relationship," "audit itself," "drifting from its mission," "check against the rules," "not trusting the output," "get stuff very clean before going agentic."

**Do:** apply when the narrator is structuring or policing agent behaviour.

**Do not:** apply when she simply notes that the tool made a mistake. That belongs to `#limit-of-the-tool`.

---

## Changelog

`2026-06-25` — Taxonomy v1 created. 8 core themes, 5 emergent themes defined.
`2026-06-26` — Taxonomy updated to v2. Full definitions added to each tag. Theoretical anchor added (Silverstone domestication theory). Application rules, linguistic anchors, and do/do not pairs added per tag. Emergent theme graduation threshold defined at 15% of total beats.
`2026-09-25` · Taxonomy updated to v3. Eight tags added from a full scan of 40 entries: `#value-visibility`, `#trust-in-the-tool`, `#cost-of-speed`, `#interest-in-the-work`, `#cost-of-access`, `#how-i-learn`, `#collaborative-transparency`, `#governing-agents`. Definitions of `#builder-identity` and `#ai-policy-friction` broadened. Recurrence threshold of 3 entries per new tag. Tags stay flat; parent themes to be derived from co-occurrence after the re-tag pass.

---

*Created by Charline x Claude — June 25, 2026 — Updated to v2: June 26, 2026 · Updated to v3: September 25, 2026*