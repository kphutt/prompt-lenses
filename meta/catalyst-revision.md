# Meta-Prompt: Revise The Catalyst

You are revising a standalone prompt called "The Catalyst." The current version and research
findings are attached. Your job is to produce a revised version that incorporates the strongest
research insights without compromising what already works.

## What The Catalyst Is

A prompt that takes any artifact (code, document, plan, system) and produces exactly one idea
to make it fundamentally better — or explicitly abstains. It is generative, not evaluative. It
is not a review tool, not a brainstorming tool, not an analysis framework. Its power comes from
the constraint: one idea, committed, or silence.

## What Makes the Current Version Work

Before you change anything, understand what you're protecting:

1. **The voice.** Direct, confident, anti-bureaucratic. Sentences are short. Paragraphs are
   short. The prompt reads like it was written by someone who has run too many meetings that
   should have been a decision. Do not turn this into a procedure manual.

2. **The constraint.** One idea. Commit or abstain. Everything in the prompt exists to enforce
   this. Any addition that dilutes the constraint — that gives the model more room to hedge,
   list, or equivocate — fails regardless of how well-researched it is.

3. **The brevity.** The current prompt is 77 lines. It is readable in under two minutes. That
   brevity is load-bearing — it means the model spends its context window on the artifact, not
   on processing instructions. A 200-line version of this prompt would be a worse prompt even
   if every line were individually good.

4. **The output format.** Clean, scannable, focused on the reader's decision: adopt this idea
   or don't. The reader does not want process documentation. They want the idea, the argument
   for it, and enough concreteness to evaluate it.

## The Five Recommended Changes

These emerged from a research survey of commitment-forcing prompts, confidence calibration,
and adjacent formats (Amazon memos, commander's intent, VC theses, design critique). Each
addresses a documented failure mode.

### Change 1: Add a Backcasting Step (STRONG RECOMMENDATION)

**What:** Before generating the idea, the model should envision the ideal version of the
artifact, then identify the single change that closes the largest gap between current and ideal.

**Why:** This is the single highest-leverage addition from the research. It addresses three
failure modes simultaneously:
- **Safe-pick bias** — by anchoring on a transformed end state, the model can't default to
  the safest incremental improvement
- **Incrementalism dressed as transformation** — the gap between current and ideal is a
  measurable standard for whether an idea is truly transformative
- **Weak abstention** — if the ideal state is barely different from the current state, that's
  a natural signal to abstain (the artifact is already good)

**Design decision required:** Should the backcasting be internal process only (the model does
it but doesn't show it) or visible in the output? The user has stated they care about the idea,
not the process. But the ideal-state framing could strengthen the "Why This Changes Things"
section naturally — the gap IS the argument. Decide which approach produces a better reader
experience.

**Source evidence:** Backcasting methodology in strategic planning; the research found no
prompt engineering implementation of this, making it a novel structural addition.

### Change 2: Add a Confidence Gate Before Generation (MODERATE RECOMMENDATION)

**What:** Separate confidence assessment from idea generation. The model first assesses whether
it has genuine signal for a transformative improvement. If not, it abstains before committing
to an idea.

**Why:** Research on Answer-Free Confidence Estimation (AFCE) shows that assessing confidence
*before* generating the answer reduces overconfidence. When confidence assessment happens
after the idea exists, sunk-cost pressure pushes the model to justify what it already wrote.
The biggest risk in the current design — per the research — is artificial confidence / failure
to abstain, because RLHF training optimizes for "produce something useful" rather than "honestly
assess whether you have something worth saying."

**Design decision required:** This is clearly an internal process instruction, not an output
section. The question is whether it can be woven into the existing Rules section naturally or
whether it needs its own step. Keep it lightweight — one or two sentences, not a procedure.

**Source evidence:** AFCE research; Wen et al. 2025 TACL survey on LLM abstention.

### Change 3: Replace Killed Darlings with Adversarial Counterargument (STRONG RECOMMENDATION)

**What:** Remove the "What I Considered and Killed" output section. Replace it with a section
where the model presents the strongest argument *against* its chosen recommendation, then
explains why the recommendation holds despite that argument.

**Why:** Two converging reasons:
- **Cognitive load (from design discussion):** The user stated they don't need proof of
  selection. They evaluate the idea on its own merits. Showing 2-3 rejected alternatives
  forces involuntary mental simulation of each one — the reader builds partial models of
  worlds they'll never visit. That's pure tax.
- **Selection quality (from research):** Multi-agent debate literature shows that adversarial
  pressure — arguing against your own recommendation — strengthens selection more effectively
  than simply listing what you rejected. The counterargument stress-tests the winner directly
  instead of comparing it to losers.

The result: one stress test to evaluate (lower cognitive load) that also strengthens the
recommendation (higher quality). The killed darlings were doing two jobs — evidence of
selection and tradeoff transparency — and the counterargument does both jobs better.

**Critical nuance from the research:** The act of *considering and rejecting alternatives*
during generation improves selection quality. This must be preserved as internal process even
though it's removed from the output. The model should still generate candidates, compare them,
and select — it just doesn't show the rejects. It shows the attack on the winner instead.

**Design decision required:** What to call this section. "Strongest Counterargument" is
accurate but clinical. "The Case Against" is punchier. "Why This Might Be Wrong" is more
natural. Choose something that fits the voice.

**Source evidence:** Du et al. 2024, Liang et al. 2024, SID framework 2025 (multi-agent
debate); VC "what would change our minds" practice.

### Change 4: Add a Safe-Pick Detector (MODERATE RECOMMENDATION)

**What:** After generating the recommendation, the model asks itself: "Is this the most
impactful idea, or the safest idea? If I chose the safe option because it felt more defensible,
I should replace it."

**Why:** Safe-pick bias is the most dangerous failure mode identified in the research — it
produces output that *looks* like commitment but is actually incrementalism dressed as
conviction. Models default to conventional, defensible suggestions when forced to choose one.
Naming the bias explicitly helps the model correct for it.

**Design decision required:** This is an internal self-check. It should not appear in the
output. The question is where to place it — as a final step before output, or woven into the
selection process alongside backcasting. Keep it to one sentence.

**Source evidence:** LLM moderation bias research; LLM-as-judge safe-pick patterns; the
anti-hedging framework (DrRockzos, Dec 2025).

### Change 5: Add Brief Deployment Guidance (LIGHT RECOMMENDATION)

**What:** One or two sentences indicating when The Catalyst is most effective — when the
artifact's fundamental approach is still a choice, not when you're deep in execution details.

**Why:** The Catalyst demands a different cognitive mode than review tools. It asks the reader
to hold two mental models (current approach vs. proposed reframing) and evaluate a paradigm
shift. Deploying it routinely on every artifact — including ones deep in execution — creates
unsustainable cognitive load even when the ideas are good. A brief signal about intended use
prevents misuse without being prescriptive.

**Design decision required:** Where does this go? Options: a short line before the Rules
section, a note at the very end, or a parenthetical in the opening. It must not feel like a
disclaimer or a user manual. One sentence, woven naturally into the voice.

## Additional Candidates to Evaluate

The research surfaced several other suggestions. For each one below, decide whether it earns
its place in the revised prompt. Apply the evaluation criteria in the next section — most of
these should probably be rejected, but evaluate honestly.

### Commander's Intent Output Format
**What it is:** Require the recommendation to include a single sentence describing what success
looks like after the change — an end state, not a task.
**Potential value:** Forces specificity and testability. If the end state sounds incremental,
the idea probably is.
**Potential cost:** Adds another output section. May overlap with "Why This Changes Things."
**Evaluate:** Does this add something the existing output format doesn't already capture?

### Role Elevation
**What it is:** Assign a specific expert role with experience markers (e.g., "principal
architect who has seen this pattern fail at three companies") to shift which patterns the
model activates.
**Potential value:** Research shows expert-level role assignment shifts token distributions
toward higher-quality outputs.
**Potential cost:** The Catalyst is currently role-agnostic — it works on any artifact type.
Adding a specific role narrows it. A generic expert role ("senior practitioner with deep
experience") adds little.
**Evaluate:** Is there a way to get the benefit without narrowing the prompt's generality?

### Anti-Hedging Permission
**What it is:** Explicitly tell the model it has permission to not hedge — that direct,
committed language is preferred over qualified language.
**Potential value:** Research suggests models hedge partly because they think they should.
Giving explicit permission to be direct may improve conviction quality.
**Potential cost:** The current prompt already does this implicitly through tone and
constraint. Adding an explicit "you don't have to hedge" instruction might be redundant.
**Evaluate:** Does the current prompt's implicit anti-hedging (through voice and constraint)
already handle this, or would an explicit statement add value?

### Context Window Decay Mitigation
**What it is:** For long artifacts, instruct the model to first characterize/summarize the
artifact before generating a recommendation, to prevent anchoring on locally salient sections.
**Potential value:** Addresses a real failure mode for long inputs.
**Potential cost:** Adds process instructions that are irrelevant for short artifacts (which
are the primary use case). Makes the prompt conditional — "if the artifact is long, do X."
**Evaluate:** Is this better handled in the prompt itself, or in usage guidance external to
the prompt?

### Narrative Forcing (Amazon Memo Style)
**What it is:** Require the recommendation as a narrative paragraph rather than structured
sections, on the theory that you can't hedge as easily in narrative form.
**Potential value:** Interesting mechanism — structure itself as a commitment device.
**Potential cost:** Would require completely redesigning the output format. The current format
is scannable and efficient. A narrative format would be harder to quickly evaluate.
**Evaluate:** Is the current structured format already commitment-forcing enough, or would
narrative produce meaningfully different outputs?

## Evaluation Criteria

For each change (recommended or additional), apply these tests:

1. **Does it address a documented failure mode?** Changes that prevent specific, named failures
   earn their place more easily than changes that are "generally good."

2. **What's the cost in lines?** Every line added to this prompt must justify itself. If a
   change requires 10 lines of instruction, it needs to be 10 lines worth of better. Estimate
   the line cost before deciding.

3. **Does it preserve the constraint?** If a change gives the model more room to hedge, list,
   or equivocate, reject it regardless of other merits.

4. **Does it preserve the voice?** Read the change aloud in the context of the existing prompt.
   If it sounds like a different author wrote it — more formal, more procedural, more cautious
   — rewrite it until it matches, or reject it.

5. **Internal process vs. output format.** Changes to what the model does internally are cheap
   (they don't increase cognitive load on the reader). Changes to the output format are
   expensive (the reader has to process them every time). Prefer internal process changes.

6. **Is it already handled implicitly?** The current prompt does a lot through voice and
   structure that it never states explicitly. If a mechanism is already working implicitly,
   adding an explicit version may weaken it by making it feel bureaucratic.

## Structural Option: One Prompt or Two?

Before revising, evaluate whether The Catalyst should remain a single prompt or become a
two-step sequence where Step 1's output feeds into Step 2.

### The Case for Two Steps

**Step 1 — Assess:** Envision the ideal version of the artifact. Measure the gap between
current and ideal. Assess confidence that a transformative improvement exists. If the gap is
small or confidence is low, stop — output a brief "no catalyst needed" with reasoning.

**Step 2 — Generate:** Given the ideal state and gap from Step 1, produce the one idea that
closes the largest gap. Full output format with counterargument and confidence.

Why this might be better:
- The AFCE research specifically found that separating confidence assessment from generation
  reduces artificial confidence. Two steps is a structural implementation of that finding.
- Step 1 becomes a natural deployment gate. You don't have to decide when to run the Catalyst
  — run Step 1 liberally, and it self-selects out when there's nothing transformative to say.
  This solves the cognitive load problem at the workflow level.
- Each prompt is shorter and more focused. The model isn't trying to assess confidence AND
  envision ideal state AND generate AND select AND stress-test in one pass.
- The user can inspect the intermediate output (the ideal state and gap assessment) before
  deciding whether to run Step 2. That's agency over the process.

### Critical Design Principle: Cascade Classifier Theory

If you choose two steps, this principle governs how to tune each step's sensitivity.

The two-step Catalyst is structurally identical to a **cascade classifier** — the pattern used
in computer vision (Viola-Jones face detection) and medical screening, where a cheap first
stage screens candidates before an expensive second stage does deep analysis. Decades of
research on these systems converge on a counterintuitive but well-proven principle:

**The cheap first stage should be a loose gate with high sensitivity, not a tight gate with
high specificity.**

This means Step 1 should be tuned to catch every artifact that genuinely has room for a
transformative idea, even if it also lets through some that don't need it. Step 1 should
almost never say "no gap" when a real opportunity exists (low false negatives), and it's
acceptable if it sometimes sends artifacts to Step 2 that turn out not to need transformation
(false positives are cheap).

The reasoning comes from asymmetric error costs:
- A **false negative** in Step 1 (saying "no gap" when a moonshot exists) is invisible and
  permanent — you walk past a transformative opportunity and never know it existed.
- A **false positive** in Step 1 (saying "gap detected" when the artifact is fine) is visible,
  cheap, and self-correcting — Step 2 either produces a mediocre idea you reject, or honestly
  abstains. Cost: one wasted prompt and two minutes of reading.

**Implication for prompt design:** Step 1's abstention threshold should be high — it should
only say "no catalyst needed" when the gap is genuinely small and clear. Any ambiguity about
whether a transformative improvement exists should result in "proceed to Step 2." The tight
filtering happens in Step 2, where the model does the expensive generative work and can
honestly abstain after deep analysis.

This means **most of the cognitive load protection comes from Step 2's honest abstention, not
Step 1's gating.** Step 1 protects against missed opportunities. Step 2 protects against
wasted cognitive effort.

Step 1 should also characterize the *type* of gap it detects, which informs Step 2's search.
Two primary gap types:
- **Structural gap:** The artifact's internal organization, architecture, or mechanics don't
  serve its purpose well. The pieces are wrong, or they're assembled wrong. Example: an auth
  system that couples session management with identity verification when they should be
  independent. The ideal version has different pieces or different relationships between them.
- **Framing gap:** The artifact's structure may be sound, but it's solving the wrong problem,
  targeting the wrong audience, or operating under an assumption that doesn't hold. Example:
  a PRD that optimizes onboarding flow when the real problem is that users don't understand
  what the product does. The ideal version starts from a different premise.

These gap types require different kinds of ideas from Step 2. A structural gap calls for
reorganization or re-architecture. A framing gap calls for redefining what the artifact is
trying to accomplish. Step 1 should flag which type it's seeing (or if it's both) so Step 2
can search in the right space.

### The Case for One Prompt

Why it might be better to keep it as a single prompt:
- Simplicity. One prompt, one output, done. The Catalyst's current appeal includes its
  operational simplicity.
- The model has full context in one pass — no information loss between steps.
- Most of the "two-step" benefits (backcasting, confidence gating) can be implemented as
  internal process instructions within a single prompt.
- Added friction may discourage use, especially for the "run Step 1 liberally" pattern.

### Your Decision

Evaluate both options against the criteria below. If two steps is clearly better, produce
both prompts. If one prompt is clearly better, produce the single revised prompt. If it's
close, produce the single prompt but note what would change in a two-step version.

## Output Requirements

Produce three things (or four, if recommending two steps):

### 1. Structural Decision: One Prompt or Two?

State your decision and reasoning. If two steps: explain exactly where the seam is and how
output from Step 1 feeds into Step 2.

### 2. Change Evaluation Table

For each of the five recommended changes AND each additional candidate, provide:
- **Decision:** Include / Exclude / Modify
- **Reasoning:** 2-3 sentences, referencing the evaluation criteria
- **If included:** Where it goes and estimated line cost
- **If two-step:** Which step it belongs in

### 3. The Revised Prompt(s)

The complete, final text. This is the deliverable.

If one prompt:
- Read as a single coherent document, not as a patched original
- Preserve the voice, constraint, and brevity of the original
- Stay under 100 lines (stretch target: under 90)
- Include all changes marked "Include" in the evaluation table

If two prompts:
- Each prompt should be self-contained and readable independently
- Step 1 should produce output that can be pasted directly into Step 2's input
- Step 2's instructions should specify what it expects as input
- Combined line count for both prompts should stay under 120 lines
- Both prompts must share the same voice

### 4. Changelog

A brief section documenting what changed and why, structured as:
- Structural decision (one or two prompts) with reasoning
- What was added (with one-line justification each)
- What was removed (with one-line justification each)
- What was modified (with one-line justification each)
- What was evaluated and rejected (with one-line reason each)
- Net line count change (original → revised)
