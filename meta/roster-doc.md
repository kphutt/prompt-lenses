You are designing the STANDARD SET of lenses that will be applied to EVERY document review.

Your output is a roster — a list of lens names with brief descriptions. You are NOT writing
the lenses themselves. A separate process will take your roster and craft each lens into a
full, high-quality prompt. Your job is to decide WHICH lenses should exist and WHY.

---

## What You're Optimizing For

This roster will be used on every document review. That means:

1. **Every lens must earn its place on MOST document types.** A lens that only matters for
   technical specs or only for strategy decks doesn't belong in the standard set. Standard
   lenses must apply to an engineering RFC, a product requirements doc, a project plan, a
   design doc, a policy document, and a business proposal.

2. **The set must be small enough to run fully every time.** Target 8-10 standard lenses.
   Every lens beyond 8 must justify why it can't be folded into another.

3. **Mandatory lenses are non-negotiable.** Certain perspectives must ALWAYS be included
   regardless of what the rest of the roster looks like. These are listed below.

---

## MANDATORY LENSES

These must appear in every standard document roster. You can refine their names and
descriptions, but the cognitive modes they represent cannot be cut or merged away.

### Security
Documents create systems, policies, and architectures. Every document that describes something
to be built, adopted, or changed has security implications — even if it doesn't mention
security. This lens asks: "What attack surfaces, vulnerabilities, or security assumptions does
this document create, ignore, or get wrong?" It should catch: architectures with unaddressed
threat models, policies that create exploitable gaps, requirements that conflict with security
principles, and the absence of security considerations where they should be present.

### Privacy
Distinct from security. This lens asks: "Does this document account for the privacy
implications of what it proposes?" This includes: data collection beyond what's needed, missing
consent mechanisms, unclear data retention, PII flowing to places it shouldn't, GDPR/CCPA/
regulatory blind spots, and the subtle one — documents that propose features or systems that
*could* be privacy-respecting but don't specify the privacy-respecting approach, leaving it
to implementers to figure out (who usually won't).

### Testability / Verifiability
The document equivalent of code testability. This lens asks: "How would you verify that what
this document describes has been achieved?" For specs: are the requirements falsifiable? For
plans: are the milestones measurable? For policies: can compliance be audited? If a document
describes a desired outcome in terms that can't be objectively measured, it will lead to
disagreements about whether it was achieved. "Improve user experience" fails. "Reduce task
completion time by 20% measured by analytics event X" passes.

### Plain Language & Readability
Documents exist to transfer understanding from the writer's head to the reader's head. This
lens examines whether the writing uses concrete nouns and vivid verbs rather than abstract
jargon, Latinate bureaucratese, or corporate filler. Prefer Anglo-Saxon root words over
French/Latin derivatives where meaning is preserved — "start" over "commence," "use" over
"utilize," "end" over "finalize," "help" over "facilitate," "need" over "requirement,"
"plan" over "strategic initiative." Also check: sentence length (can each sentence be parsed
in one read?), paragraph focus (one idea per paragraph?), and whether the document uses
concrete nouns and vivid verbs or hides behind abstractions and nominalizations ("we performed
an analysis of" vs. "we analyzed").

---

## EXISTING LENSES TO EVALUATE

The following lenses have been developed through iteration and are strong candidates for the
standard roster. For each one, decide: KEEP (as-is or refined), MERGE (fold into another), or
CUT (not universal enough for the standard set — move to custom/optional).

1. **🎯 The Executive** — Busy decision-maker triaging 50 docs a week. Does the thesis arrive
   in the first paragraph? Does every section survive the "so what?" cascade? Does the ending
   create forward motion with specific actions?

2. **🔍 The Skeptic** — Opposing counsel. Puts claims on a credibility spectrum, hunts weasel
   words, constructs the counter-argument the document ignores, checks evidence quality and
   causal logic.

3. **🛠️ The Implementer** — Has to build this tomorrow using only this document. Runs the
   "start tomorrow" simulation, converts vibes to specifications, finds contradictions by
   building from both ends, tests priority signals.

4. **👽 The Outsider** — Found this through search with zero context. Hits undefined terms
   like walls, traces the dependency chain of understanding, tests narrative independence,
   checks the document's self-awareness of its own scope and currency.

5. **✂️ The Editor** — Must cut to 60% length with zero meaning loss. Finds structural
   redundancy, times the runway before takeoff, exposes agency-hiding passive voice, applies
   the substitution test for filler.

6. **🔗 The Connector** — Reads between the lines for gaps. Identifies unstated dependencies,
   finds perspective gaps by inverting the author's role, walks logical stepping stones,
   generates predictable follow-up questions.

7. **🪞 The Consistency Checker** — Eidetic memory, zero tolerance for contradiction. Builds
   terminology registries, cross-verifies numbers, detects confidence-level shifts, finds
   version ghosts and scope creep.

---

## YOUR PROCESS

### Step 1: Map the mandatory lenses against the existing lenses

For each mandatory lens (Security, Privacy, Testability, Plain Language), determine:
- Does an existing lens already cover it?
- If yes, should it be kept as-is, or does the mandatory requirement expand its scope?
- If no, it needs to be added as a new lens.

Be careful with mapping. The Skeptic checks evidence quality but doesn't specifically probe
for security blind spots. The Implementer checks specificity but doesn't specifically check
whether requirements are falsifiable/testable. Don't force-merge lenses that require different
cognitive modes.

Also consider whether a mandatory lens might PARTIALLY overlap with an existing lens. In that
case, decide: expand the existing lens, or keep both with clear boundaries. The test is whether
a single reviewer can maintain both cognitive modes simultaneously. If holding "is this
argument well-reasoned?" and "does this create a security gap?" at the same time would dilute
both, they should be separate lenses.

### Step 2: Evaluate each existing lens for universality

For each of the 7 existing lenses, ask:
- "Would this lens produce meaningful findings on an engineering RFC?"
- "Would this lens produce meaningful findings on a product requirements doc?"
- "Would this lens produce meaningful findings on a project plan?"
- "Would this lens produce meaningful findings on a policy document?"
- "Would this lens produce meaningful findings on a business proposal?"
- "Would this lens produce meaningful findings on a post-mortem?"

If a lens consistently fails the universality test for 2+ document types, it shouldn't be in
the standard set. Move it to optional/custom.

### Step 3: Look for gaps

With the mandatory lenses placed and existing lenses evaluated, ask:
- "What failure mode would slip through ALL of these lenses?"
- "What cognitive mode is missing from this set?"
- "If I reviewed 100 documents with this set, what class of problem would I consistently miss?"

Common gaps in document review:

- **Audience mismatch** — partially in Outsider, but there's a distinct failure where a document
  is written for one audience but will be read by another (e.g., a technical doc that leadership
  will use for decisions)
- **Temporal validity** — does the document account for when it will become stale? Is there a
  review cadence? Will the recommendations still hold in 6 months?
- **Risk and failure modes** — documents that propose actions but don't address what happens if
  the actions fail, or what risks they create
- **Ethical implications** — beyond privacy, does the document consider fairness, bias,
  accessibility, environmental impact, or other ethical dimensions?
- **Stakeholder impact** — who is affected by this document's proposals, and are their
  perspectives represented?
- **Operationalizability** — can the thing this document describes actually be executed, monitored,
  and maintained in practice, or does it describe a desired state without a path to get there?

Don't add a lens for every gap. Only add one if: (a) the failure mode is common enough to appear
in most document reviews, (b) it requires a genuinely different cognitive mode than existing
lenses, and (c) it can't be adequately handled by expanding an existing lens's scope.

### Step 4: Check the set

Run these checks on your final roster:

**Size check**: 8-10 lenses. If more, justify. If fewer, check for gaps.

**Overlap check**: For each pair, ask "would these two lenses frequently produce the same
finding?" If yes, merge or clarify the boundary.

**Cognitive diversity check**: List the core thinking mode of each lens. Are there at least 4
genuinely different modes?

**The boring doc test**: Imagine a straightforward meeting summary or status update. Does every
lens still have something to look at? (Note: "this lens found no issues" is valid. "This lens
doesn't apply" means it shouldn't be standard.)

**The critical doc test**: Imagine a proposal to migrate the company's core infrastructure to
a new platform. Does the set collectively cover every way this document can fail catastrophically?

**The "applied all suggestions" test**: Since the user typically wants to apply ALL suggestions
from ALL lenses (not just the top findings), check that the volume of output is manageable.
If 10 lenses each produce 3-5 findings, that's 30-50 items — borderline. Make sure each lens
is focused enough that its findings are high-signal, not padded.

---

## OUTPUT FORMAT

```
## Standard Document Lens Roster

### Mandatory Lenses
[For each: name, emoji, 2-3 sentence description of the cognitive mode, and whether it maps
to an existing lens or is new]

### Retained Existing Lenses
[For each: name, emoji, 2-3 sentence description, any refinements from the original]

### New Lenses
[For each: name, emoji, 2-3 sentence description, which gap it fills, why it can't be merged
into an existing lens]

### Cut/Optional Lenses
[Any existing lenses moved out of the standard set, with explanation]

### Final Roster (ordered)
[Numbered list: emoji + name + one-sentence description]
[Note any recommended ordering — e.g., "run structural lenses first, then content lenses"]

### Gaps Acknowledged
[Failure modes that the standard set knowingly doesn't cover, and when to add a custom lens
for them]
```

---

## IMPORTANT REMINDERS

- You are producing a ROSTER, not full lens definitions. Keep descriptions to 2-3 sentences.
- Every lens must represent a distinct COGNITIVE MODE — how you think, not what you check.
- The mandatory lenses (Security, Privacy, Testability, Plain Language) cannot be cut or merged
  out of existence. They can be renamed or combined with an existing lens only if the combined
  lens genuinely activates both cognitive modes.
- Documents fail differently than code. Don't port code-review thinking to document review.
  Code fails in execution. Documents fail in comprehension, decision-making, and alignment.
- The user typically applies ALL suggestions, not just the top 3. This means every finding from
  every lens needs to be actionable and worth implementing. The anti-padding principle is even
  more important here — a lens that generates 5 "meh" findings per document will pollute
  every review.
- Prefer fewer, deeper lenses over more, shallower ones.
