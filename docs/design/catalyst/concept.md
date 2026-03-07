# The Catalyst: Complete Concept Document

## Document Purpose

This document captures the full state of thinking, research, design decisions, and open
questions around "The Catalyst" — a standalone prompt engineering tool for generating
transformative ideas. It covers the original prompt design, the research landscape that
informed it, a design discussion that revealed fundamental cognitive load problems, the
resulting architectural evolution from a single prompt to a multi-step pipeline, and
several theoretical frameworks borrowed from computer science and medical screening that
now underpin the design.

This is not a summary. It is a comprehensive record of everything discussed, discovered,
and decided, including dead ends, open questions, and speculative directions that haven't
been tested yet.

---

## Part 1: What The Catalyst Is

### 1.1 Core Concept

The Catalyst is a standalone prompt — not a review tool, not a brainstorming tool, not an
analysis framework — that takes any artifact (code, document, plan, system, process) and
produces exactly one idea to make it fundamentally better, or explicitly abstains. It is
generative, not evaluative.

The word "fundamentally" is load-bearing. The Catalyst is not looking for improvements. It
is not looking for bug fixes, optimizations, or polish. It is looking for the kind of idea
where someone reads it and says "oh — yes, obviously, why didn't we think of that?" The
kind that reframes the whole effort, or unlocks a capability that wasn't on the table, or
removes a constraint everyone assumed was fixed.

### 1.2 The Three Core Mechanisms

The Catalyst's power comes from three interlocking constraints that, according to the
research conducted, have never been combined in a published prompt engineering pattern:

**Mechanism 1: Single Output Constraint.** The prompt produces exactly one idea. Not two,
not a list, not options. One. If the model has several candidates, it must pick the one with
the highest leverage and kill the rest. The discipline of choosing one is the entire point.
This runs counter to how most people use AI — they want options, exploration, volume. The
Catalyst deliberately rejects that paradigm.

**Mechanism 2: Commitment Forcing.** The model must commit to its recommendation. It is not
generating options for someone else to pick from. It is picking. This is the difference
between brainstorming (which produces volume) and decision-making (which produces commitment).
The prompt explicitly prohibits hedging language — if the model catches itself writing
"additionally" or "another option would be," it has slipped into list mode and must stop.

**Mechanism 3: Explicit Abstention.** If the model doesn't have an idea it would bet on — one
it believes would genuinely elevate the artifact — it must say so and stop. "I don't have
one" is a valid and respected output. A mediocre idea dressed up as a great one is worse than
silence. This mechanism is critical because RLHF training optimizes models for helpfulness,
which means "produce something useful" rather than "honestly assess whether you have something
worth saying." The abstention option works against the model's training incentives, which is
exactly why it needs to be structurally enforced.

### 1.3 The Current Prompt (v1)

The complete text of The Catalyst as it exists before revision:

```markdown
# The Catalyst

You are given an artifact — code, a document, a plan, a system, a process. Your job is not
to review it. Not to find what's wrong. Not to improve what exists.

Your job is to find the one idea that would make this fundamentally better.

Not incrementally better. Not "add error handling" or "clarify section 3." The kind of idea
where someone reads it and says "oh — yes, obviously, why didn't we think of that?" The kind
that reframes the whole effort, or unlocks a capability that wasn't on the table, or removes
a constraint everyone assumed was fixed.

## Rules

**You produce exactly one idea.** Not two. Not a list. One.

If you have several candidates, pick the one with the highest leverage — the one that would
change the most about how this artifact works, reads, or is used. Kill your darlings. The
discipline of choosing one is the entire point.

**You must be confident.** If you don't have an idea that you'd bet on — one that you believe
would genuinely elevate this project — say so and stop. "I don't have one" is a valid and
respected output. A mediocre idea dressed up as a great one is worse than silence.

**You explain why it matters.** Not just what the idea is, but what changes because of it.
What becomes possible that wasn't before? What gets simpler? What falls away? The idea
should have a "because" that's as compelling as the idea itself.

**You are concrete.** Not "consider a more modular architecture." Instead: "Extract the
validation logic into a standalone pipeline that other teams can import independently —
right now it's locked inside your API handler, which means every team that needs validation
is duplicating it or depending on your deploy schedule."

## Output

## 💡 The Idea

[One sentence. Clear enough to fit in a subject line.]

### Why This Changes Things

[2-4 sentences. What becomes possible, simpler, or fundamentally different. This is the
argument — not that the idea is clever, but that it matters.]

### What It Would Look Like

[A concrete sketch. For code: what changes structurally. For a doc: what the reframed
version would contain. For a plan: what the new sequence would be. Enough to see it,
not enough to build it.]

### Confidence

[High / Medium]
[If Medium: what you'd need to verify before committing to this idea.]
[If you can't reach at least Medium: don't produce the idea. Say "I don't have one for
this artifact" and explain what you considered and why nothing cleared the bar.]

### What I Considered and Killed

[2-3 runner-up ideas, each one line: the idea and why it lost to the winner.]
[This section is evidence of selection, not a list of suggestions. Each entry must include
a specific reason the candidate is lower-leverage than the chosen idea.]
[If only one idea came to mind, say so — that's honest, not weak.]

## What This Is Not

This is not a review. Don't produce findings, severity ratings, or improvement lists. If you
catch yourself writing "additionally" or "another option would be," stop — you've slipped into
list mode. Return to the constraint: one idea, the best one, or nothing.

This is not brainstorming. Brainstorming produces volume. This produces commitment. You are
not generating options for someone else to pick from. You are picking. The "What I Considered
and Killed" section exists to show your reasoning, not to smuggle in a list — every entry
there is a rejection, not a recommendation.
```

### 1.4 How The Catalyst Was Created

The Catalyst emerged from the prompt-lenses project — a model-agnostic library of specialized
review prompts organized as "lenses," each representing a distinct cognitive perspective for
reviewing code and documents. During that work, a need became apparent for something that
wasn't a review tool — something generative rather than evaluative. The lenses find what's
wrong; the Catalyst finds what could be fundamentally different.

The prompt was refined through self-application: the Catalyst was run on itself. That
self-application produced the "What I Considered and Killed" section — the Catalyst's own
idea for improving itself was to make its selection process visible. The specific output from
the self-application run:

> "💡 The Idea: Add a 'What I Considered' section that shows the runner-up ideas that were
> killed — not to present options, but to prove the winner earned its spot."

The prompt was then reviewed using three lenses from the prompt-lenses project (Executive,
Editor, Connector). One typo was fixed. The structure was confirmed as intentionally different
from the lens template — generative prompts don't need Criteria sections the way evaluative
lenses do.

### 1.5 The Catalyst's Relationship to Prompt-Lenses

The Catalyst is NOT a lens. This distinction is important:

- Lenses are evaluative — they find problems, inconsistencies, gaps, and issues within an
  artifact's current frame. They say "here's what's wrong, fix it."
- The Catalyst is generative — it produces a new idea that doesn't exist in the artifact yet.
  It says "here's what could be fundamentally different."

Lenses operate within the artifact's assumptions. The Catalyst questions those assumptions.
This means they serve different cognitive functions and should be deployed at different points
in a workflow (more on this in Part 4).

The Catalyst lives at `catalyst.md` in the prompt-lenses project outputs but is a standalone
tool, not part of the lens roster.

---

## Part 2: The Research Landscape

### 2.1 Research Methodology

A comprehensive research prompt was designed to survey everything relevant to The Catalyst
across six categories. The research prompt itself went through lens review (Executive, Skeptic,
Implementer) and two refinements were made:

1. Added 16 specific search terms across domains, because the concept spans multiple fields
   that don't share vocabulary (commitment-forcing prompts, confidence calibration, design
   critique, military doctrine, venture capital, etc.)
2. Softened scarcity bias in the instructions: changed from "you won't find a perfect match"
   to "direct matches may be rare, but look hard before concluding they don't exist."

The research was conducted using OpenAI's tools due to their strength in voluminous content
generation and broad search capability.

### 2.2 Research Categories and Findings

#### Category 1: Commitment-Forcing Prompts & Frameworks

**Overall finding:** Very little exists that specifically forces LLMs to commit to a single
recommendation with an abstention option. The prompt engineering space is overwhelmingly
focused on getting better outputs — longer, more accurate, better formatted — not on forcing
singular committed outputs. This is a genuine gap in the landscape.

**The Pyramid Principle (Minto/McKinsey).** The closest structural analog in communication
design. Barbara Minto's framework from the 1960s: start with the answer first, support with
grouped arguments, back with data. Several practitioners have adapted this into LLM system
prompts. The mechanism that forces commitment is structural — by requiring the answer to come
first, the model can't build toward a safe hedge. It has to lead with conviction. This has
been tested with LLMs and works.

**Self-Evaluation Gating.** A pattern from production prompt engineering: ask the model to
rate its own answer on a 1-10 scale, then only accept outputs above a threshold (typically 9).
This is a quasi-commitment mechanism. Key insight from practitioners: models behave like
humans and default to the easiest answer rather than the best one. An explicit quality standard
forces them to reach further. Close to The Catalyst's confidence gating but oriented toward
quality rather than conviction about a specific idea.

**Tree of Thoughts (ToT) with Selection.** The model explores multiple reasoning branches,
evaluates each, and selects the best. The selection step is a form of commitment-forcing.
However, ToT is oriented toward reasoning correctness (math, logic puzzles), not generative
ideation. The evaluation criteria would need complete redesign for The Catalyst's use case.
The mechanism — branch, evaluate, select — is relevant, but the application domain is wrong.

**The Anti-Hedging Framework (DrRockzos, Dec 2025).** A Hacker News poster reported a prompt
framework targeting LLM hedging, tested across Claude, GPT-5, Grok, Llama, Gemini, Mistral,
and Qwen/DeepSeek. The mechanism: give the model an explicit choice between "default alignment
(hedging-first)" and "logical coherence (truth-first)." Every model reportedly chose logical
coherence when offered the choice. The poster's theory: hedging "injects low-information
tokens that dilute attention gradients and give the model permission to drift." Unverified and
unpublished beyond a provisional patent, but the hypothesis that permission to not hedge
improves output quality aligns with what The Catalyst does structurally.

**What doesn't exist:** There is no widely-adopted prompt pattern that says "give me exactly
one idea, commit to it or say nothing." The reason is likely that most users want options from
their AI. Forcing a single committed answer is a power-user pattern that runs counter to the
default interaction model.

#### Category 2: Elevation / "10x" Thinking Prompts

**Overall finding:** Plenty of human frameworks exist (10x thinking, first principles
reasoning, assumption invalidation). Almost none have been rigorously adapted for LLMs in
ways that demonstrably produce transformative rather than incremental outputs.

**First Principles Prompts.** Multiple templates on marketplaces attempt to operationalize
Musk-style first principles thinking. Typical pattern: "Break down [problem] into fundamental
elements, question each assumption, rebuild from scratch." These do produce different outputs
than "how can I improve X" but they suffer from a structural weakness: they produce a
reframing but not a committed recommendation. Output is still "here are approaches you could
consider" — still a list, still hedged.

**Assumption Invalidation Prompting.** Extract assumptions from a model, then systematically
invalidate them one by one. Produces genuinely different thinking by forcing the model to
explore the problem space without default constraints. Tested with GPT-4. Weakness: produces
multiple alternative framings, not a single committed idea. It's divergent, not convergent.

**The Inversion Pattern.** Instead of asking the model to execute a task, provide content and
ask the model to analyze, critique, or challenge it. Role reversal activates different
analytical capabilities. Directly relevant to The Catalyst because the prompt needs the model
to look at an artifact from outside its current frame.

**Role Assignment at Expert Level.** Specific, expert-level role assignment (e.g., "direct
response copywriter with 25%+ open rates" rather than just "copywriter") shifts which token
distributions the model samples from. Relevant for elevation — assigning roles like "principal
architect who has seen this pattern fail at three companies" would access different knowledge.

**What's missing:** Nobody has combined "10x not 10%" framing with a commitment mechanism. You
can find prompts that push for transformative thinking, and separately prompts that force
selection, but the combination doesn't exist as a published pattern.

#### Category 3: Pre-Mortem / Inversion Prompts

**Pre-Mortem as Human Framework.** Gary Klein's technique, popularized by Kahneman: imagine
the project has failed spectacularly, then work backward to identify why. The mechanism is
psychological safety — easier to name risks when framed as imaginary post-failure analysis.

**Pre-Mortem Adapted for AI (Lightly).** Some practitioners use pre-mortem prompts with LLMs.
Works for risk identification but used defensively, not generatively. The gap: using pre-mortem
as a lens to identify the highest-leverage intervention point, not just risks.

**Backcasting.** The inverse of pre-mortem: imagine the ideal successful outcome, then work
backward to identify what had to be true. Well-documented in strategic planning. As a prompt
pattern: "Describe the perfect version of this system. Now identify the single change that
would move the current version closest to that ideal." This pattern doesn't appear in prompt
engineering literature as a named technique but maps directly onto a key mechanism The Catalyst
could use. This became the single strongest recommendation from the research.

**Reverse Step-by-Step Prompting.** An OpenAI community post from August 2024 proposed reverse
engineering solutions by thinking in steps backward. Untested but the underlying concept is
sound.

#### Category 4: Confidence Calibration & Selective Abstention

**Overall finding:** This is where the most rigorous academic work exists, but it's almost
entirely oriented toward factual Q&A accuracy, not generative ideation. The abstention research
is about "don't answer when you don't know the facts," not "don't recommend when you don't
have a genuinely good idea."

**"Know Your Limits" Survey (Wen et al., 2025, TACL).** The definitive survey paper on LLM
abstention. Key finding: abstention can be approached from three perspectives — the query (is
it answerable?), the model (does it have the knowledge?), and human values (should it answer?).
Important insight for The Catalyst: most abstention research assumes there's a correct answer
the model might not know. The Catalyst's abstention case is different — it's about whether the
model has a sufficiently good idea, which is harder to calibrate.

**SelectLLM (2025, OpenReview).** End-to-end method integrating selective prediction into
fine-tuning. Not directly applicable to a standalone prompt but principles inform design.

**Answer-Free Confidence Estimation (AFCE).** A critical finding: separating confidence
estimation from answer generation produces better-calibrated confidence scores. The method
asks the model to rate its confidence on a question BEFORE answering it, then asks for the
answer separately. This reduces overconfidence and produces more human-like sensitivity to
task difficulty. Directly applicable to The Catalyst: asking "how confident are you that you
can identify a transformative improvement?" before generating the idea might produce more
honest abstention. This became one of the key recommended changes and a primary argument for
the two-step architecture.

**Verbalized Confidence vs. Actual Accuracy.** Multiple papers find that asking models to state
confidence percentages is poorly calibrated — models tend toward overconfidence. The implication:
The Catalyst's confidence mechanism should probably not ask for a numeric score but instead use
structural signals as implicit confidence indicators.

**Consistency-Based Methods.** Several approaches use multiple samples to estimate confidence —
if the model gives different answers when asked the same question multiple times, confidence
should be lower. Suggests a mechanism: run ideation multiple times internally and only output
if the same recommendation emerges consistently.

#### Category 5: "Killed Darlings" / Reasoning Transparency Patterns

**Chain-of-Thought for Decision-Making.** CoT is well-established for reasoning tasks but its
application to selection among alternatives is much less developed. Standard CoT says "show
your work on how you reached the answer." The Catalyst's killed darlings asks "show what you
rejected and why." Showing rejected alternatives is a form of negative reasoning that doesn't
have a standard prompt pattern.

**Multi-Agent Debate Systems.** Significant academic work (Du et al., 2024; Liang et al., 2024;
SID framework 2025) uses multiple LLM agents arguing different positions to improve answer
quality. The mechanism: adversarial pressure forces each agent to strengthen its arguments and
find weaknesses in alternatives. Key insight for The Catalyst: the act of explicit comparison
sharpens selection. Having the model argue against alternatives produces higher-quality final
selections. This became a key argument for replacing killed darlings with adversarial
counterargument.

**Self-Reflection Patterns.** Two-step pattern: generate → critique → regenerate. Reasoning
transparency for quality. Adapting it for selection — "here are three possible ideas, here's
why each one fails or succeeds, here's why this one wins" — would be a novel application.

**Self-Consistency (Wang et al., 2022).** Sample multiple reasoning paths and take majority
vote. The principle applies: generating multiple candidate ideas and selecting the most
consistent/strongest could improve commitment quality.

#### Category 6: Adjacent Art

**Amazon's 6-Pager / One-Pager Memo Culture.** The memo requires a narrative making a
recommendation, not a slide deck presenting options. The forcing function is the narrative
form itself — you can't hedge in a six-page narrative the way you can in a bullet-point deck
with pros/cons columns. The author must commit to a position and argue for it.

**McKinsey's Pyramid Principle (Minto).** The Pyramid Principle works because it inverts the
natural order of thinking. You think bottom-up (data → analysis → conclusion) but present
top-down (conclusion → arguments → data). This inversion forces commitment — you must have
your answer before you can present anything.

**Commander's Intent.** A clear, concise statement of what success looks like — the "why" and
the "end state," deliberately omitting the "how." The power: it empowers action in the absence
of detailed instructions. Must be "easy to remember and clearly understood two echelons down."
Structural elements that produce conviction: brevity (forces prioritization), purpose-first
(why before how), and end-state clarity (concrete vision of success).

**Venture Capital Thesis Documents.** A single bet, fully argued. The forcing function: you're
putting money behind it, so the analysis must be conviction-weighted, not balanced. The "what
would change our minds" section is structurally identical to The Catalyst's killed darlings
concept.

**Design Critique Culture.** In strong design cultures, critique sessions force a "one
direction" decision. The mechanism: the critique isn't about whether the design is good but
about which direction to take. Prohibition of compromise is itself a design choice that
produces better outcomes.

### 2.3 Mechanisms That Work (Cross-Category)

The research identified six mechanisms with evidence of effectiveness:

1. **Answer-First Structural Forcing** — By requiring the recommendation first, the model
   can't build toward a hedge. The Catalyst partially uses this but could strengthen it.

2. **Explicit Permission to Abstain** — Paradoxically, giving the model an off-ramp improves
   the quality of its commitments. Without an abstention option, models fill the space with
   something safe. The Catalyst already has this and it's one of its strongest mechanisms.

3. **Negative Reasoning / Explicit Rejection** — The act of arguing against alternatives
   sharpens selection. It's not enough to pick the best — you must articulate why the
   alternatives lose. The Catalyst has this via killed darlings.

4. **Inversion / Outside-Frame Viewing** — Forcing the model to view the artifact from a
   different temporal or analytical frame breaks default optimization-within-current-frame.
   The Catalyst does this implicitly but not structurally.

5. **Role Elevation** — Expert-level role assignment shifts token distributions toward
   higher-quality outputs. The Catalyst doesn't currently include role assignment.

6. **Confidence Separation** — Assessing confidence before generating the recommendation
   produces more honest self-assessment. The Catalyst doesn't currently separate these.

### 2.4 Documented Failure Modes

**Failure Mode 1: Safe-Pick Bias.** When forced to choose one idea, models default to the
safest, most conventional option rather than the most transformative one. This is the most
dangerous failure mode because it produces output that looks like commitment but is actually
incrementalism dressed as conviction. The Catalyst partially handles this through its
"fundamentally better" instruction but lacks a structural mechanism to detect it.

**Failure Mode 2: Hedging Disguised as Commitment.** The model produces what looks like a
single recommendation but embeds hedges: "The most impactful change would be X, though Y
and Z are also worth considering." The killed darlings section may help by providing an
outlet for the model's impulse to cover alternatives.

**Failure Mode 3: Artificial Confidence.** The model generates a recommendation with high
stated confidence not because it has genuine signal but because the prompt requires confidence.
RLHF training specifically rewards helpful, complete answers, working against honest abstention.
This is the biggest risk in the current design.

**Failure Mode 4: Elevation Without Grounding.** Transformative-sounding idea that's actually
vague, impractical, or disconnected from the actual artifact. "Rewrite the entire architecture
using event sourcing" sounds transformative but may be obvious or impractical. The gap between
"conceptually different" and "concretely better" is large.

**Failure Mode 5: Context Window Decay.** In longer artifacts, the model loses track of the
full picture and optimizes for a local improvement rather than the globally most impactful
change. Well-documented attention degradation in long contexts.

### 2.5 Honest Assessment of Originality

The research concluded that The Catalyst is genuinely novel in combination, though not in
individual components. The commitment-forcing mechanism exists nowhere in published prompt
engineering as a deliberate design choice for generative ideation. The killed darlings concept
has analogs in VC thesis documents and multi-agent debate, but its application as a
transparency mechanism in a single-shot generative prompt is original. The abstention mechanism
draws from academic work on LLM calibration, but that work is almost entirely focused on
factual Q&A, not creative/strategic ideation.

The space is remarkably empty. Most prompt engineering is about getting models to produce more.
The Catalyst is about getting models to produce less — one thing, with conviction. This is a
genuinely different design philosophy, and the landscape suggests almost nobody is exploring
it deliberately.

---

## Part 3: The Cognitive Load Problem

### 3.1 Discovery

This problem was discovered at the end of the session where The Catalyst was created. The
conversation was cut off mid-discussion, making it the primary open thread carried into the
current session.

### 3.2 The Core Tension

Review lenses and The Catalyst demand fundamentally different cognitive modes from the user.

A review lens says: "Line 47 has a consistency issue." The user looks at it, agrees or
disagrees, and moves on. This is a two-step cognitive process: evaluate the finding, decide
to act or not. Low cognitive load.

The Catalyst says: "What if this whole thing were organized around X instead?" Now the user
is holding two mental models simultaneously — the current approach and the proposed
reframing — simulating the rewrite mentally, evaluating a delta they can't fully see yet.
That's five or more cognitive steps, and each one is expensive.

Running The Catalyst on everything would be exhausting even when the ideas are good. This is
a design problem about human capacity to process transformative ideas, not a usage problem.

### 3.3 Three Distinct Problems Hidden in One

Analysis revealed that the cognitive load problem contains three independent sub-problems:

**Problem 1: When to deploy.** The Catalyst is a strategic tool, not a routine one. The
question is whether deployment timing should be specified in the prompt itself or in external
workflow documentation. Resolution: the user's instinct is that deployment timing will emerge
from experience and can't be fully predicted yet. The pattern appears to be: use it when the
artifact's fundamental approach is still malleable — brainstorm docs, PRDs, architecture docs,
key decision points. Not on every artifact, not routinely.

**Problem 2: Whether the killed darlings section helps or hurts.** The "What I Considered and
Killed" section was designed to build trust in the selection process. But the user reported
they don't need proof of selection — they evaluate the idea on its own merits. The section
creates involuntary cognitive load: the reader mentally simulates each rejected alternative
even as they read why it was rejected. The reader builds partial models of worlds they'll
never visit. That's pure tax.

Further analysis revealed the section was doing two jobs simultaneously:
- **Evidence of selection quality** (the model actually thought about alternatives) — cheap
  to process, the reader just needs to see that alternatives existed
- **Tradeoff transparency** (here's the landscape of options) — expensive to process, the
  reader absorbs the tradeoff landscape whether they want to or not

The user's clear statement: "I'll use the idea or not... I don't really care about seeing
evidence of the work." This resolved the question: the section is overhead for this user.

**Problem 3: Sequencing in a workflow.** The Catalyst might belong at a specific point in a
review workflow — either before or after lenses. This connects to existing research on lens
ordering, which found that macro changes before micro and that tool order significantly
affects effectiveness.

### 3.4 Resolution of Problem 2: Killed Darlings

Two options were identified:

**Option A (recommended): Move to internal process, remove from output.** Tell the model to
consider and reject alternatives as part of its reasoning, but only output the winning idea.
The selection quality benefit (from multi-agent debate research) accrues during generation,
not during the user's reading. The model could do the comparison work without showing it.

**Option B: Replace with adversarial counterargument.** Instead of 2-3 rejected alternatives
(three mental models to simulate), show one attack on the winner (one stress test to evaluate).
This is multi-agent debate compressed into a single agent. The model steelmans the opposition
to its own recommendation. If it can't survive its own best counterargument, the recommendation
is weak.

The adversarial counterargument approach was identified as superior because it's lower
cognitive load (one stress test vs. three rejected alternatives) and arguably more useful
(tells the user the biggest risk of the idea they're about to adopt).

### 3.5 Resolution of Problem 3: Tool Ordering

The analysis converged on: **Catalyst first, then lenses.**

The Catalyst is the most macro tool in the workflow. It asks "is the whole approach right?"
Lenses then clean up within the chosen frame. Running lenses first and then discovering via
Catalyst that the whole frame is wrong means the lens passes were wasted effort.

This connects to the existing lens ordering research: macro changes should come before micro.
The Catalyst is the most macro intervention available.

One caveat from the research: Failure Mode 5 (context window decay) means the Catalyst works
better on shorter, early-stage artifacts that the model can hold in full context. This aligns
with the deployment timing instinct — brainstorm docs, PRDs, and architecture docs are
typically shorter than finished codebases.

For very long artifacts, a summarization step before the Catalyst might be needed, which could
mean a specific lens pass to characterize the artifact before the Catalyst runs.

---

## Part 4: The Two-Step Architecture

### 4.1 How It Emerged

The two-step architecture emerged from the convergence of three insights:

1. The AFCE research showing that separating confidence assessment from answer generation
   reduces artificial confidence
2. The backcasting recommendation (envision ideal state, measure gap) being a naturally
   different cognitive task from idea generation
3. The deployment timing problem — needing a way to know when to run the expensive generative
   step without requiring the user to manually judge every artifact

### 4.2 Step 1: Assess

Step 1 reads the artifact and performs backcasting: envisions the ideal version of the
artifact, then measures the gap between current and ideal state. Three possible outcomes:

**Small gap.** The artifact is already close to its ideal form. No room for a transformative
idea. Incremental improvements might exist, but that's what lenses are for. Step 1 stops
here: "No catalyst needed."

**Large gap, clear shape.** The ideal version looks substantially different from the current
version, and the nature of the difference is visible — structural, framing, or both. Step 1
reports the gap and its character. Step 2 fires.

**Large gap, unclear shape.** The model can tell the artifact is far from ideal but can't
clearly articulate what the ideal looks like. This is the most honest abstention case — "I
sense this could be much better but I can't see how."

### 4.3 Step 2: Generate

Step 2 receives Step 1's output (the ideal state description and gap characterization) and
produces the one idea that closes the largest gap. Full output format with counterargument
and confidence.

### 4.4 What Step 1 Is Actually Doing

Step 1 is not predicting whether a brilliant idea exists. It can't — nobody can see an idea
before it's found. What it's doing is measuring the gap between what the artifact is and what
it could be. These are different tasks.

The mechanism concretely: the model reads the artifact, then asks "what would the ideal version
of this look like?" That's a cheap cognitive task — you're not designing the solution, you're
imagining the destination. Like looking at a house and saying "the ideal version of this has
an open floor plan, natural light from the south side, and the kitchen flows into the living
space" without knowing which walls are load-bearing or what it would cost to move the plumbing.

Then it compares the two pictures.

The honest limitation: the model's ideal vision is bounded by its own knowledge. It might see
a small gap not because the artifact is great, but because it can't imagine a radically
different version. Step 1 can produce false negatives. But this is the same limitation that
exists in the single-prompt version — at least in the two-step version, the false negative
is cheap.

### 4.5 Why Two Steps Is Better Than One

- Confidence assessment separated from generation (AFCE principle) reduces artificial
  confidence — the biggest risk in the current design
- Step 1 becomes a natural deployment gate — run it liberally, it self-selects out when
  there's nothing transformative to say
- Each prompt is shorter and more focused — the model isn't trying to assess, envision,
  generate, select, and stress-test in one pass
- The user can inspect intermediate output (ideal state and gap) before deciding to run Step 2
- Step 1's backcasting provides a concrete evaluation framework for Step 2 — "closes the
  largest gap between current and ideal" is measurable in a way "fundamentally better" isn't

---

## Part 5: Cascade Classifier Theory and Asymmetric Error

### 5.1 The Bloom Filter Analogy

An analogy to Bloom filters was identified during the design discussion. A Bloom filter's
guarantee is asymmetric error: it can say "definitely not in the set" with certainty, or
"maybe in the set" with some false positive rate. Zero false negatives, controlled false
positives.

Step 1 of the Catalyst has the **opposite error profile:**

- Step 1's "yes, there's a gap" is probably trustworthy — if the model can see a large
  distance between current and ideal, there's almost certainly room for improvement
- Step 1's "no, the gap is small" is the unreliable signal — the model might fail to envision
  a radically better version, not because one doesn't exist, but because it's outside the
  model's imagination

A Bloom filter: "no" is reliable, "yes" needs verification.
Step 1: "yes" is reliable, "no" might be wrong.

The shared DNA between the two: **cheap pre-filter gating an expensive operation.** Both are
asking "should I spend the resources on the real computation?" Both accept an error rate on
one side to make the filter fast.

The difference in which side the error falls on matters for workflow design: when Step 1 says
"large gap, run Step 2," trust that signal. When Step 1 says "small gap, skip" — hold it
lightly. If gut instinct says "there's something here the model isn't seeing," run Step 2
anyway.

### 5.2 The Inverse Bloom Filter

Research confirmed that a data structure with the exact error profile of Step 1 exists: the
Inverse Bloom Filter, originally designed by Jeff Hodges for deduplicating event streams. An
Inverse Bloom Filter may report a false negative but can never report a false positive. Step 1
has the same shape: "yes, there's a gap" is high-confidence (you've definitely seen the
opportunity space), but "no gap detected" might just mean the filter wasn't sophisticated
enough to see it.

### 5.3 Cascade Classifier Theory

The two-step Catalyst is structurally identical to a cascade classifier — the pattern used
in computer vision (Viola-Jones face detection, 2001) and medical screening. The Viola-Jones
face detector used 38 stages with just 1 feature in the first stage, then 10, 25, 25, 50 in
subsequent stages. The first stages remove unwanted candidates rapidly to avoid paying the
computational costs of later stages.

Decades of research on cascade classifiers converge on a counterintuitive but well-proven
principle: **the cheap first stage should be a loose gate with high sensitivity, not a tight
gate with high specificity.**

This means each early stage must validate all true positives and can produce many false
positives. Early cheap stages are deliberately tuned for high sensitivity (catch everything
real) at the cost of low specificity (let some junk through). Later expensive stages clean
up the false positives.

### 5.4 Application to the Catalyst

**Step 1 should be tuned for high sensitivity** — it should flag every artifact that genuinely
has room for a transformative idea, even if it also flags some that don't need it.

**Step 2 is the expensive stage** that sorts real signal from false positives through honest
abstention.

This is the opposite of the naive instinct. The naive instinct is that Step 1 should be a
tight gate — only let through artifacts that really need transformation. Cascade classifier
theory says the cheap stage should be a loose gate with high recall. Let it be generous. The
expensive stage is where you get picky.

### 5.5 Asymmetric Error Costs

The reasoning comes from medical screening theory on sensitivity/specificity tradeoffs. The
cutoff choice for any screening test depends on a value judgment about the cost of false
positives versus false negatives.

For the Catalyst:

**False negative cost (Step 1 says "no gap" when a moonshot exists):** Invisible and permanent.
You walk past a transformative opportunity and never know it existed. You keep going with your
current approach, unaware it could have been fundamentally better. This is the expensive error.

**False positive cost (Step 1 says "big gap" when the artifact is fine):** Visible, cheap, and
self-correcting. You run Step 2 unnecessarily. Step 2 either produces a mediocre forced
recommendation (which you reject) or honestly abstains. Cost: one wasted prompt and two
minutes of reading.

The asymmetry is clear: **false negatives are much more expensive than false positives.**

### 5.6 Design Implications

1. Step 1's abstention threshold should be high — it should only say "no catalyst needed" when
   the gap is genuinely small and clear. Any ambiguity should result in "proceed to Step 2."
2. Step 2's abstention mechanism is where strict filtering happens. This is where the AFCE
   confidence separation earns its keep.
3. Most of the cognitive load protection comes from Step 2's honest abstention, not Step 1's
   gating. Step 1 protects against missed opportunities. Step 2 protects against wasted
   cognitive effort.

---

## Part 6: Structural Gaps vs. Framing Gaps

### 6.1 The Distinction

Step 1's backcasting naturally reveals two fundamentally different types of gaps between an
artifact's current state and its ideal state.

**Structural gap:** The artifact's internal organization, architecture, or mechanics don't
serve its purpose well. The pieces are wrong, or they're assembled wrong. The artifact might
be solving the right problem but solving it badly.

Examples:
- An auth system that tightly couples session management with identity verification. Both
  subsystems work. But because they're coupled, you can't change how sessions expire without
  touching identity logic, and every team that needs identity has to also take a dependency
  on your session model. The ideal version has the same capabilities but different boundaries.
- A PRD that puts the technical architecture section before the user problem statement. All
  the content is correct, but the reader has to hold implementation details before understanding
  why any of it matters. The ideal version has the same content, reorganized.
- A house where the kitchen is on the third floor and the dining room is in the basement.
  Every room works individually. The arrangement means anyone who cooks dinner walks two
  flights of stairs to serve it.

Structural gaps call for **reorganization** — same purpose, better machinery.

**Framing gap:** The artifact's machinery might be fine, but it's pointed at the wrong target.
The artifact is solving the wrong problem, making the wrong assumption, or addressing the
wrong audience.

Examples:
- A beautifully engineered recommendation engine that optimizes for click-through rate when
  the actual business problem is retention. The code is clean, the architecture is sound, the
  algorithm is sophisticated. But it's optimizing the wrong metric.
- A PRD with a flawless onboarding flow design — clear steps, good UX, smooth progression.
  But the real reason users drop off isn't that onboarding is confusing. It's that they don't
  understand what the product is before they start. The ideal version doesn't have a better
  onboarding flow. It has a fundamentally different acquisition strategy.
- A house that's beautifully built, efficient layout, everything flows. But it's a
  single-family home in a neighborhood that desperately needs multi-unit housing. The
  construction is excellent. The premise is wrong.

Framing gaps call for **redefinition** — different purpose, potentially different machinery.

### 6.2 Why This Distinction Matters

**They require different search strategies.** A structural solution asks "how should this be
reorganized?" — the destination stays the same, the route changes. A framing solution asks
"should this be going somewhere else entirely?" — the route might be fine, the destination
is wrong.

**Framing gaps are higher leverage but harder to see.** A structural gap is visible from inside
the artifact — you can see the coupling, the misorganization, the inefficiency. A framing gap
requires stepping outside the artifact and questioning its assumptions. This is exactly what
backcasting does: the ideal version of an artifact with a framing gap looks fundamentally
different in purpose, not just in structure.

**Most models default to finding structural gaps.** Structural improvements are safer, more
concrete, more defensible. "Decouple these two systems" is an easier recommendation than
"you're solving the wrong problem." The safe-pick detector exists partly for this reason.

**An artifact can have both.** If it does, the framing gap takes priority — fixing the
structure of an artifact that's pointed at the wrong target is wasted work.

### 6.3 The Catalyst's Unique Value is Framing

This is a critical insight from the design discussion. Looking at the full tool ecosystem:

- Lenses catch structural issues — consistency problems, implementation gaps, coupling
- Code review catches structural issues
- The user's own engineering eye catches structural issues
- Multiple tools ask "is this built well?"
- **Zero tools ask "should this exist in its current form?"**

The Catalyst is the only thing in the pipeline that steps outside the artifact and questions
its premise. That's its marginal value over everything else. If it comes back with a structural
recommendation, it might be good, but it's doing a job lenses could also do. If it comes back
with a framing insight, it's doing a job nothing else in the workflow does.

This doesn't mean the Catalyst should only detect framing gaps. It means the Catalyst should
have a **natural bias toward framing insights** because that's where it adds value that no
other tool provides. The safe-pick detector should specifically ask: "Am I recommending a
structural improvement because it's genuinely the highest leverage, or because it's easier to
see and more defensible than a framing insight I haven't looked hard enough for?"

### 6.4 Gap Type Detection Is Natural, Not Classified

Step 1 doesn't need a separate classification step for gap type. The type of gap is inherent
in what the ideal version looks like — it's a byproduct of backcasting.

If the ideal version the model envisions is "the same system but with auth and sessions
decoupled" — that's structural. The purpose is identical, the machinery is different.

If the ideal version is "a retention tool, not an onboarding flow" — that's framing. The
purpose shifted.

Step 1 just needs to describe the ideal version clearly, and the gap type reveals itself in
the description.

---

## Part 7: The Three-Step Pipeline (Speculative)

### 7.1 Evolution from Two Steps to Three

A further architectural refinement was proposed: separating gap assessment from gap
classification from idea generation. Each step does exactly one cognitive task.

**Step 1 — Assess:** See the gap. Describe the ideal state, measure the distance, characterize
what's different. No classification burden, no generation burden. Just look and describe.

**Step 2 — Route:** Read Step 1's description and decide what kind of problem this is.
Structural, framing, or both. Pure analysis — reading a description and making a judgment
call. Can think hard about that one question because it's not doing anything else.

**Step 3a — Structural Specialist:** Generate within a known structural gap. Fully dedicated
to reorganization, re-architecture, and mechanical improvements. Doesn't waste attention on
premise questions.

**Step 3b — Framing Specialist:** Generate within a known framing gap. Fully dedicated to
questioning premises, assumptions, and purpose. Doesn't waste attention on structural
possibilities.

### 7.2 Why Three Steps Might Outperform Two

Classification quality scales with dedicated attention. When gap-type classification is a side
output of Step 1, it gets whatever attention is left over after the backcasting work. When it's
the entire job of Step 2, the model can weigh ambiguous signals, consider whether what looks
structural is actually a symptom of a framing problem, and make a genuinely thoughtful routing
decision.

The question "is the structural issue actually a symptom of a framing problem?" is the hardest
one in the whole system, and it deserves its own thinking step.

### 7.3 The Router Pattern

The architecture is a router pattern — Step 1 is a dispatcher, not just a gate. It assesses
the gap, Step 2 classifies it, and the system routes to a specialized handler. Each specialist
prompt gets to be sharper because it's doing one job.

```
Step 1 (Assess)
  → "No gap" → stop
  → Gap detected → Step 2 (Route)
    → "Structural" → Step 3a (structural specialist)
    → "Framing" → Step 3b (framing specialist)
    → "Both" → Step 3b first (framing priority), then optionally 3a
    → "Unclear" → general-purpose Step 3 or run both specialists
```

### 7.4 Tradeoff

Three steps is more friction than two, which is more friction than one. But if this heads
toward automation (see Part 8), the friction is only a problem during manual R&D. Once it's
a pipeline, three API calls is trivially different from two.

### 7.5 Current Status

This architecture is speculative. The decision was made to NOT include the three-step option
in the meta-prompt for v2 revision. Instead: run the meta-prompt as-is, let it decide between
one and two steps, see what comes out. Then iterate to three steps as a follow-on if two-step
wins — splitting assessment from routing is a clean refactor once Step 1's output format is
defined.

---

## Part 8: Automation and Infrastructure (Side Quest)

### 8.1 The Vision

The two-step (or three-step) architecture makes automation possible in a way the single-prompt
version doesn't. A monolithic Catalyst that runs on everything is expensive and noisy. A cheap
Step 1 that runs on everything and an expensive Step 2 that runs selectively — that's an
architecture that scales.

### 8.2 Possible Implementations

**Google Apps Script + Gemini API.** The user is already building inbox-shepherd with Apps
Script. The same infrastructure could watch a Google Drive folder. When a doc lands in a
specific folder, a script triggers an API call with Step 1. If the response indicates a gap,
it either triggers Step 2 automatically or sends a notification.

**Claude API with tool use.** Step 1 runs, parses its own output for the gap signal, and
conditionally calls Step 2. The prompt could be designed so Step 1 outputs structured JSON
that the orchestrator reads programmatically.

**Git hooks.** For code artifacts: a git pre-commit or post-commit hook runs Step 1 against
changed files. If it finds a gap, it opens a GitHub issue or drops a comment.

### 8.3 Design Question: User Visibility

The fundamental question: does the human see Step 1's output, or only Step 2's?

If only Step 2's output (or "no gap found"), the system is fully automated and the cascade
works cleanly. Step 1 is invisible plumbing.

If the human sees Step 1 too, that's additional cognitive load but gives veto power.

Recommended approach: show Step 1's output only when it fires, and make it one sentence.
Something like: "Architecture-v3: large structural gap detected — current design couples
auth and session management in ways the ideal version wouldn't. Running deep analysis."

### 8.4 Current Status

This is explicitly parked as a future infrastructure concern. The meta-prompt focuses on
getting the prompts right. The infrastructure does whatever it has to do to support whatever
the R&D produces.

---

## Part 9: The Meta-Prompt for Revision

### 9.1 Purpose

A meta-prompt was created to drive the revision of The Catalyst v1 into v2. It is designed
to be fed to an LLM alongside the current catalyst.md and catalyst-research.md.

### 9.2 What the Meta-Prompt Contains

**Grounding section:** What The Catalyst is and what makes the current version work (voice,
constraint, brevity, output format). This prevents the reviser from "improving" the prompt
in ways that destroy what already works.

**Five recommended changes with evidence:**

1. **Add a backcasting step (STRONG)** — Envision ideal state, identify gap. Addresses
   safe-pick bias, incrementalism, and weak abstention simultaneously.
2. **Add a confidence gate before generation (MODERATE)** — Separate confidence assessment
   from idea generation per AFCE research.
3. **Replace killed darlings with adversarial counterargument (STRONG)** — Lower cognitive
   load, higher selection quality. One stress test instead of three rejected alternatives.
4. **Add a safe-pick detector (MODERATE)** — "Is this the most impactful idea or the safest?"
   One-sentence self-check.
5. **Add brief deployment guidance (LIGHT)** — When the frame is still a choice, not deep
   in execution.

**Five additional candidates to evaluate:**

1. Commander's Intent output format
2. Role elevation
3. Anti-hedging permission
4. Context window decay mitigation
5. Narrative forcing (Amazon memo style)

**Evaluation criteria (deliberately brutal):**

1. Does it address a documented failure mode?
2. What's the cost in lines? (Every line must justify itself)
3. Does it preserve the constraint?
4. Does it preserve the voice?
5. Internal process vs. output format (prefer internal)
6. Is it already handled implicitly?

**Structural decision: one prompt or two?** The meta-prompt forces the reviser to evaluate
both options and decide before making any changes. Arguments for both are presented.

**Cascade classifier design principle:** If two steps is chosen, Step 1 must be a loose gate
with high sensitivity (catch every opportunity, accept false positives) and Step 2 must be
the strict filter (honest abstention protects against cognitive load). This section includes
the full asymmetric error cost analysis and the structural vs. framing gap taxonomy.

**Output requirements:**
1. Structural decision with reasoning
2. Change evaluation table (include/exclude/modify for each change)
3. The revised prompt(s) — complete text, not patches
4. Changelog documenting everything that changed and why

**Constraints:** Single prompt must stay under 100 lines (stretch: 90). Two prompts combined
must stay under 120 lines. Voice must be preserved throughout.

### 9.3 What the Meta-Prompt Does NOT Contain

- The three-step pipeline architecture (deferred to follow-on iteration)
- Automation/infrastructure considerations (separate concern)
- The Bloom filter / Inverse Bloom Filter theoretical framework (informed the design
  principles but the principles themselves are what the meta-prompt uses)

---

## Part 10: The Catalyst in the Broader Prompt-Lenses Project

### 10.1 Project Context

The prompt-lenses project is a model-agnostic library of specialized review prompts organized
as "lenses." The system uses a three-layer meta-prompt architecture: prompts that generate the
lens roster, prompts that ensure lens quality, and the lenses themselves. The project is
currently at Phase 2.2 (shared fragments) on its roadmap.

### 10.2 Catalyst's Position in the Project

The Catalyst is a standalone tool, not a lens. It lives alongside the lens system but operates
on different principles:

- Lenses are evaluative → The Catalyst is generative
- Lenses find problems → The Catalyst finds opportunities
- Lenses work within the artifact's frame → The Catalyst questions the frame
- Lenses are routine (run on every artifact) → The Catalyst is strategic
- Lenses produce multiple findings → The Catalyst produces exactly one idea or nothing

### 10.3 Three New Lens Candidates from Earlier Work

During the session where The Catalyst was created, three new lens candidates were identified
for Phase 3 evaluation:

1. **Bug Finder** — dedicated "find what's broken" lens (code + doc)
2. **Smooth Handoff** — will the next person trip over this? (doc, maybe code)
3. **Toil Detector** — manual effort that could be automated (code + doc)

### 10.4 A Possible New Lens: Premise Checker

During the current design discussion, a potential new tool was identified: a lightweight
"premise checker" that isn't the Catalyst but addresses framing gaps specifically. It would
be simpler, cheaper, and run earlier and more often than the Catalyst. It would only ask
"does this artifact's stated goal match the actual problem it should be solving?"

This could be a lens rather than a standalone tool — it's evaluative (checking a specific
property) rather than generative (producing a new idea). It would complement the Catalyst
by flagging framing issues during routine review, while the Catalyst handles the deeper
generative work of producing the transformative idea when framing problems are detected.

This is an undesigned concept — just a direction identified during discussion.

---

## Part 11: Open Questions and Unresolved Threads

### 11.1 One Step vs. Two Steps vs. Three Steps

The meta-prompt asks the reviser to decide between one and two steps. The three-step pipeline
is deferred. The result of the meta-prompt run will determine the next iteration.

### 11.2 How Step 1 Actually Performs

No testing has been done. All of the two-step architecture is theoretical. Key unknowns:
- Does backcasting actually produce meaningfully different ideal-state descriptions for
  different artifacts?
- Does the gap size assessment correlate with whether Step 2 produces good ideas?
- How often does Step 1 produce false negatives (missing real opportunities)?
- How often does Step 1 produce false positives (sending fine artifacts to Step 2)?

### 11.3 Whether Specialized Prompts (3a/3b) Actually Outperform a General Prompt

The hypothesis that a framing-only prompt and a structural-only prompt outperform a
general-purpose Step 2 is untested. It's theoretically grounded (dedicated attention,
no competing search strategies) but might not matter in practice.

### 11.4 The Safe-Pick Problem at Scale

Even with a safe-pick detector, models may still default to structural recommendations over
framing insights because structural ideas are easier to generate, more concrete, and feel
more defensible. This is a deep alignment problem that a prompt instruction may not fully
solve.

### 11.5 Calibrating Step 1's Sensitivity

Cascade classifier theory says Step 1 should be a loose gate with high sensitivity. But how
loose? Too loose means Step 2 runs on everything (defeating the purpose of the gate). Too
tight means missing moonshots. The right calibration will only emerge from testing.

### 11.6 The Framing Gap Lens

The idea of a lightweight "premise checker" lens (distinct from the Catalyst) was identified
but not designed. It might be worth exploring during Phase 3 of the prompt-lenses project
when new lens candidates are evaluated.

### 11.7 Automation Architecture

The infrastructure for running Step 1 automatically (Google Apps Script, git hooks, API
orchestration) was identified as feasible but parked. The prompt design must be finalized
first.

---

## Part 12: Concept Relationships and Alternative Names

### 12.1 What The Catalyst Would Be Called in Other Fields

The Catalyst concept doesn't have a single name in any established field, but it touches
several established concepts:

- **Commitment-forcing prompt** (prompt engineering) — the single-output constraint
- **Generative ideation tool** (design thinking) — produces new ideas, not evaluations
- **Backcasting with commitment** (strategic planning) — envision ideal, find the gap
- **Single-thesis document** (venture capital) — one bet, fully argued
- **Commander's intent derivation** (military) — define the end state, not the plan
- **Elevation prompt** (prompt engineering) — "10x not 10%" thinking
- **Selective prediction with abstention** (ML research) — commit or refuse to answer
- **Cascade pre-filter** (computer vision) — cheap screen before expensive analysis
- **Opportunity detector** (informal) — finds where transformative ideas could live
- **Frame validator** (informal) — questions whether the artifact's premise is correct

### 12.2 Related Concepts From This Discussion

- **Prompt pipeline** — multi-step prompt architecture where each step's output feeds the next
- **Cognitive load management** — designing AI tool outputs to match human processing capacity
- **Tool sequencing** — the order in which AI review tools are applied affects their
  effectiveness (macro before micro)
- **Asymmetric error tolerance** — accepting higher error rates on one side to minimize
  errors on the other side (from Bloom filters, cascade classifiers, medical screening)
- **Gap taxonomy** — structural gaps (wrong machinery) vs. framing gaps (wrong target)
- **Router pattern** — a classification step that dispatches to specialized handlers
- **Safe-pick bias** — models defaulting to conventional recommendations when forced to choose

---

## Part 13: Files and Deliverables

### 13.1 Files Produced

| File | Purpose | Status |
|------|---------|--------|
| catalyst.md | The current Catalyst prompt (v1) | Complete, awaiting revision |
| research-prompt-catalyst.md | Instructions for conducting the research survey | Complete, already executed |
| catalyst-research.md | Full research results across 6 categories | Complete |
| process-catalyst-research.md | Prompt for analyzing research through 3 design questions | Complete, superseded by meta-prompt |
| meta-prompt-revise-catalyst.md | Meta-prompt for producing Catalyst v2 | Complete, ready to run |

### 13.2 Next Steps

1. Run the meta-prompt with catalyst.md and catalyst-research.md attached
2. Evaluate the output — particularly the structural decision (one vs. two steps)
3. If two-step: test Step 1 on several real artifacts to see how gap assessment performs
4. If three-step architecture is pursued: refactor based on meta-prompt results
5. Build findings document incorporating meta-prompt results with this concept document
6. Consider premise-checker lens for Phase 3 evaluation

---

## Part 14: Key Insights (Index)

For reference, the major insights from this work in order of discovery:

1. The Catalyst occupies genuinely novel territory — no published prompt combines single
   output, commitment forcing, and abstention for generative ideation
2. The biggest risk is artificial confidence / failure to abstain (RLHF works against it)
3. The single highest-leverage addition is backcasting before generation
4. Killed darlings should be removed from output (cognitive load) but preserved as internal
   process (selection quality)
5. Adversarial counterargument is superior to killed darlings for both quality and cognitive
   load
6. The Catalyst should run before lenses (macro before micro)
7. Separating confidence assessment from generation (two-step) reduces artificial confidence
8. Step 1 has an Inverse Bloom Filter error profile — "yes" is reliable, "no" might be wrong
9. Cascade classifier theory: Step 1 should be loose (high sensitivity), Step 2 strict
10. False negatives (missed moonshots) are far more expensive than false positives (wasted
    Step 2 runs)
11. Two types of gaps: structural (wrong machinery) and framing (wrong target)
12. Framing gaps are the Catalyst's unique value — nothing else in the workflow questions
    premises
13. The Catalyst should bias toward framing insights because structural insights are the
    path of least resistance
14. Gap type reveals itself through backcasting — no separate classifier needed
15. A three-step pipeline (assess → route → specialize) may outperform two steps by giving
    gap classification dedicated attention
