You are conducting a focused research dive on **generative ideation prompts** — prompts,
frameworks, and tools that produce a single high-leverage idea rather than reviewing,
analyzing, or listing. This is specifically about: what exists in the space of
commitment-forcing, elevation-oriented AI prompts, and what can we learn from it?

## Context

I've built a standalone prompt called "The Catalyst" that takes any artifact (code, document,
plan, system) and produces exactly one idea to make it fundamentally better — not incrementally,
not a list of suggestions, one committed recommendation with high confidence or explicit
abstention. It includes a "killed darlings" section showing runner-up ideas and why they lost.

This is a different animal from review or analysis prompts. It's generative, not evaluative.
The constraint (one idea, commit or abstain) is the core mechanism. I need to know what else
exists in this space so I can sharpen it.

## What I Need You To Find

### 1. Commitment-Forcing Prompts & Frameworks

Anything that deliberately constrains AI output to a single recommendation, decision, or
idea rather than producing lists or options. This includes:

- Prompts that force ranking and selection rather than enumeration
- Decision-making frameworks adapted for AI use (not just "list pros and cons")
- "Best single answer" patterns — how do people get models to commit rather than hedge?
- Anything that uses an abstention mechanism ("if you can't be confident, say nothing")

For each one:
- What it is and where to find it
- How it forces commitment (what's the mechanism?)
- Does it actually work, or does the model still hedge and list?
- What's clever about the constraint design

### 2. Elevation / "10x" Thinking Prompts

Prompts or frameworks designed to produce transformative rather than incremental ideas.
This includes:

- "10x not 10%" thinking prompts (from Astro Teller / Google X philosophy, or similar)
- Reframing prompts — things that ask the model to challenge assumptions, not optimize
  within them
- First-principles prompts that strip away convention to find better approaches
- Prompts from product strategy, innovation, or design thinking adapted for AI
- Any prompt that explicitly distinguishes "better" from "fundamentally different"

For each one:
- The approach and how it pushes past incremental thinking
- Whether it's been tested with LLMs or is adapted from human frameworks
- Whether it produces concrete output or vague inspiration

### 3. Pre-Mortem / Inversion Prompts

Prompts that work by thinking backwards from an ideal state or a failure state. Related to
The Catalyst because both require the model to see the artifact from outside its current
frame. This includes:

- Pre-mortem prompts ("imagine this failed — why?") used generatively rather than defensively
- "Ideal state" prompts ("describe the perfect version, then identify the one change to get
  closer")
- Inversion techniques ("what would make this twice as bad? Now invert it.")
- Backcasting frameworks adapted for AI use

### 4. Confidence Calibration & Selective Abstention

How do people get models to accurately assess their own confidence and abstain when
appropriate? This includes:

- Research on LLM confidence calibration (2023-2025)
- Prompts that produce well-calibrated confidence scores
- Abstention mechanisms — how do you get a model to say "I don't have a good answer" instead
  of fabricating one?
- Any research on whether asking models to rate their confidence actually improves output
  quality or just adds a number

### 5. "Killed Darlings" / Reasoning Transparency Patterns

Prompts or techniques that make the model's selection process visible — not just the output
but why alternatives were rejected. This includes:

- Chain-of-thought patterns adapted for decision-making (not just reasoning)
- "Show your work" for selection, not computation
- Debate or adversarial selection patterns where the model argues with itself
- Any research on whether showing rejected alternatives improves the quality of the chosen one
  (does the act of explicit comparison sharpen the selection?)

### 6. Adjacent Art

Things that aren't prompts but embody the same principle — a single, committed,
high-conviction output. Looking for structural inspiration:

- Amazon's "one-pager" and "6-pager" memo culture (single recommendation, not options)
- McKinsey's "answer first" communication (lead with the recommendation)
- "Commander's intent" in military planning (one clear statement of what success looks like)
- Venture capital "thesis" documents (one bet, fully argued)
- Design critique culture — how designers force "one direction" decisions rather than
  committee compromise

For each:
- What makes the format work for forcing commitment
- What structural elements produce conviction rather than hedging
- What can be adapted into prompt design

## How To Conduct This Research

1. **This is a niche topic.** Direct matches may be rare, but look hard before concluding
   they don't exist. The best insights will come from combining a commitment-forcing technique
   from one domain with a confidence calibration approach from another.

2. **Search broadly with varied terms.** This concept spans multiple fields that don't share
   vocabulary. Try: "force LLM to choose one answer," "single recommendation prompt," "AI
   decision making commit," "prompt abstention mechanism," "10x thinking AI prompt," "first
   principles prompt engineering," "pre-mortem prompt LLM," "confidence calibration LLM 2024,"
   "best single answer prompt design," "Amazon one-pager decision format," "commander's intent
   product strategy," "reframing prompt engineering," "prompt constraint forcing," "LLM
   selective abstention," "chain of thought decision making," "adversarial self-debate prompt."

2. **Prioritize things that have been tested with LLMs.** Frameworks designed for humans are
   interesting but I need to know what actually works when an AI runs it. If you find a human
   framework that seems promising but untested with AI, flag it as "untested but worth trying."

3. **Look for the failure modes.** When people try to get models to commit to one idea, what
   goes wrong? Does the model hedge? Pick the safest option instead of the best one? Produce
   incrementalism dressed as transformation? Understanding the failures is as important as
   finding successes.

4. **Be honest about the landscape.** This might be a space where very little exists. If so,
   say that — it's a useful finding. "Nobody seems to be doing this well" is a valid and
   important conclusion.

## Output Format

### Section 1: The Landscape (What Exists)

For each category above, the best finds with full details. Rank by relevance to The Catalyst.
If a category has nothing good, say so and explain why (is it because nobody's tried, or
because people tried and it doesn't work?).

### Section 2: Mechanisms That Work

Across everything found, what are the specific mechanisms that successfully force commitment,
produce elevation rather than incrementalism, or calibrate confidence? List each mechanism
with evidence and assess whether The Catalyst already uses it or should incorporate it.

### Section 3: Failure Modes

What goes wrong when people try to do what The Catalyst does? Common failure patterns, with
specific examples if possible. For each failure mode, assess whether The Catalyst's current
design handles it.

### Section 4: Structural Ideas to Steal

Specific structural elements from any source that could improve The Catalyst. Not vague
inspiration — concrete additions, modifications, or reframings, with reasoning for each.

### Section 5: Honest Assessment

- How original is The Catalyst's approach? Is this well-trodden ground or genuinely novel?
- What's the strongest version of this concept that the research suggests is possible?
- What's the single biggest risk in The Catalyst's current design?
- If you had to make one change to the prompt based on this research, what would it be?
