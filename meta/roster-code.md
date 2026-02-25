You are designing the STANDARD SET of lenses that will be applied to EVERY code review.

Your output is a roster — a list of lens names with brief descriptions. You are NOT writing
the lenses themselves. A separate process will take your roster and craft each lens into a
full, high-quality prompt. Your job is to decide WHICH lenses should exist and WHY.

---

## What You're Optimizing For

This roster will be used on every code review. That means:

1. **Every lens must earn its place on MOST codebases.** A lens that only matters for web apps
   or only for distributed systems doesn't belong in the standard set. It can be a custom lens.
   Standard lenses must apply to a Python script, a React component, a Kubernetes config, a
   CLI tool, an API server, and a data pipeline.

2. **The set must be small enough to run fully every time.** If there are 15 lenses, reviewers
   will skim. If there are 7, they'll engage with each one. Target 8-10 standard lenses. Every
   lens beyond 8 must justify why it can't be folded into another.

3. **Mandatory lenses are non-negotiable.** Certain perspectives must ALWAYS be included
   regardless of what the rest of the roster looks like. These are listed below.

---

## MANDATORY LENSES

These must appear in every standard code roster. You can refine their names and descriptions,
but the cognitive modes they represent cannot be cut or merged away.

### Security
Every piece of code has an attack surface. Even internal tools, even scripts, even libraries.
The security lens must think like an attacker — not run a checklist of OWASP items but actively
try to break, abuse, and exploit the code. It should chain small observations into attack
narratives and probe the gap between what the code assumes and what it enforces.

### Privacy
Distinct from security. Security asks "can an attacker get in?" Privacy asks "is data being
collected, stored, transmitted, retained, or exposed in ways that violate user expectations,
regulations, or ethical norms?" This includes: PII handling, data minimization, consent
boundaries, logging of sensitive data, retention policies, cross-border data flow, right to
deletion compliance, and whether the code collects more than it needs. Privacy failures are
often legal liabilities, not just technical bugs.

### Testability
Not "are there tests?" but "CAN this code be tested well?" This is about the architecture's
relationship to provability — are dependencies injectable, is logic separable from side effects,
are boundaries clean enough to test in isolation? And where tests exist: do they prove behavior
or just exercise code? Could you introduce a realistic bug and have the tests catch it?

### Plain Language & Readability
Code is read 10x more than it's written. This lens examines whether names, comments, and
documentation use concrete nouns and vivid verbs rather than abstract jargon, Latinate
bureaucratese, or unnecessarily technical terms. Prefer Anglo-Saxon root words over
French/Latin derivatives where meaning is preserved — "start" over "initiate," "use" over
"utilize," "end" over "terminate," "show" over "demonstrate," "get" over "retrieve." This
extends to function names, variable names, error messages, comments, commit messages, and
documentation. The standard: could a smart person who's not an expert in this domain read
the identifiers and comments and roughly follow what's happening?

---

## EXISTING LENSES TO EVALUATE

The following lenses have been developed through iteration and are strong candidates for the
standard roster. For each one, decide: KEEP (as-is or refined), MERGE (fold into another), or
CUT (not universal enough for the standard set — move to custom/optional).

1. **🗡️ The Adversary** — Hostile actor composing attack chains from small observations.
   Traces trust boundaries, simulates state corruption, probes auth gaps.

2. **👶 The Newcomer** — First-week engineer. What would mislead me, confuse me, or cause me
   to introduce a bug? Reads names as promises, measures tribal knowledge debt, tests
   modification radius.

3. **⏳ The Time Traveler** — Visiting from 2 years in the future. What seeds of rot, scaling
   walls, and assumption hardening are planted now? Projects dependency futures and API regret.

4. **🔧 The Operator** — 3 AM on-call. Can I diagnose what's wrong and fix it without making
   it worse? Tests observability, failure blast radius, recovery paths, error hierarchy.

5. **🔬 The Specification Lawyer** — Takes names, types, comments, and docs as sworn testimony.
   Finds where the implementation breaks the promises the interface makes. Breaks invariants,
   interrogates type-level lies.

6. **🧹 The Deleter** — Every line must justify its existence. Prosecutes abstractions, finds
   duplicated logic in different clothes, measures complexity-to-value ratio, examines
   dependency weight.

7. **🧪 The Scientist** — Evaluates the evidentiary basis for believing this code is correct.
   Maps confidence topology, tests the tests, identifies untestable architecture, probes error
   path coverage.

8. **🌊 The Flow Analyst** — Follows data from birth to death. Tracks transformations, finds
   validation gaps after transformation, maps consistency boundaries, traces cleanup paths.

---

## YOUR PROCESS

### Step 1: Map the mandatory lenses against the existing lenses

For each mandatory lens (Security, Privacy, Testability, Plain Language), determine:
- Does an existing lens already cover it? (e.g., The Adversary covers Security)
- If yes, should it be kept as-is, or does the mandatory requirement expand its scope?
- If no, it needs to be added as a new lens.

Be careful: "covers" means the cognitive mode genuinely encompasses the mandatory concern.
The Adversary covers security attacks but might NOT cover privacy — an attacker's goals and
a privacy auditor's goals are different. Don't force-merge lenses that require different
thinking modes.

### Step 2: Evaluate each existing lens for universality

For each of the 8 existing lenses, ask:
- "Would this lens produce meaningful findings on a 50-line Python script?"
- "Would this lens produce meaningful findings on a 10,000-line API server?"
- "Would this lens produce meaningful findings on infrastructure-as-code?"
- "Would this lens produce meaningful findings on a data transformation pipeline?"
- "Would this lens produce meaningful findings on a CLI tool?"

If a lens consistently fails the universality test for 2+ artifact types, it shouldn't be in
the standard set. Move it to optional/custom.

### Step 3: Look for gaps

With the mandatory lenses placed and existing lenses evaluated, ask:
- "What failure mode would slip through ALL of these lenses?"
- "What cognitive mode is missing from this set?"
- "If I reviewed 100 codebases with this set, what class of problem would I consistently miss?"

Common gaps that show up:
- **Performance / efficiency** — none of the existing lenses explicitly think about computational
  cost, memory usage, or algorithmic complexity as a primary concern
- **Concurrency / distributed systems** — partially covered by Adversary (state corruption) and
  Flow Analyst (consistency) but not as a primary cognitive mode
- **Error handling philosophy** — Operator touches this, but there's a distinct cognitive mode
  around "what is the error contract of this code?"
- **API design / interface quality** — partially in Spec Lawyer and Time Traveler, but the
  specific "is this a good interface for its consumers?" question might deserve its own lens
- **Compliance / regulatory** — beyond privacy, does the code meet domain-specific requirements?

Don't add a lens for every gap. Only add one if: (a) the failure mode is common enough to appear
in most code reviews, (b) it requires a genuinely different cognitive mode than existing lenses,
and (c) it can't be adequately handled by expanding an existing lens's scope.

### Step 4: Check the set

Run these checks on your final roster:

**Size check**: 8-10 lenses. If more, justify each one beyond 10. If fewer, check for gaps.

**Overlap check**: For each pair, ask "would these two lenses frequently produce the same
finding?" If yes, merge or clarify the boundary.

**Cognitive diversity check**: List the core thinking mode of each lens. Are there at least 4
genuinely different modes? (e.g., adversarial, temporal, empathetic, reductive, investigative,
systematic)

**The boring code test**: Imagine the most boring, straightforward CRUD controller. Does every
lens still have something to look at? If a lens draws a blank on simple code, it's either too
specialized or poorly scoped. (Note: "this lens found no issues" is a valid outcome, but "this
lens doesn't even apply to this type of code" means it shouldn't be standard.)

**The critical code test**: Imagine authentication middleware for a payments system. Does the
set collectively cover every way this code can fail catastrophically? If there's a catastrophic
failure mode that no lens catches, add one.

---

## OUTPUT FORMAT

```
## Standard Code Lens Roster

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
[Note any recommended ordering — e.g., "run these first because they're most likely to find
critical issues"]

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
- Prefer fewer, deeper lenses over more, shallower ones.
- The roster should feel inevitable — a reader should look at it and think "yes, obviously
  these are the right perspectives."
