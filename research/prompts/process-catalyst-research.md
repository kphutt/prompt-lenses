# Process Catalyst Research Results

You're helping me analyze research results about commitment-forcing, elevation-oriented AI
prompts. The research was conducted using the methodology in `research-prompt-catalyst.md`
to inform the design of a standalone prompt called "The Catalyst" (`catalyst.md`). Both files
are attached.

## What The Catalyst Does

Takes any artifact (code, document, plan, system) and produces exactly one idea to make it
fundamentally better — not incrementally, not a list. One committed recommendation with high
confidence or explicit abstention.

## Three Open Design Questions

Read the research results through these three lenses. These emerged from a design discussion
about cognitive load — the Catalyst demands a different cognitive mode than review tools
(holding two mental models simultaneously, evaluating a paradigm shift) and we need to get
the deployment and structure right.

### 1. Should the "What I Considered and Killed" section be removed or reduced?

Current state: The prompt includes a section showing 2-3 runner-up ideas with rejection
reasons. Original intent was to prove selection quality.

The problem: The user doesn't need proof of selection. They'll read the idea and decide on
its merits. The killed darlings section creates involuntary cognitive load — you mentally
simulate each rejected alternative even as you read why it was rejected.

What to look for in research: Do any commitment-forcing formats include or exclude reasoning
transparency? When they include it, does it help or hurt? Is there evidence that showing
rejected alternatives improves the quality of the chosen one (justifying the cost), or is it
just process theater?

### 2. Where does Catalyst sit in a tool ordering relative to review lenses?

Current thinking: Catalyst runs FIRST, before review lenses. It's the most macro tool — it
asks "is the whole approach right?" Lenses then clean up within the chosen frame. Running
lenses first risks wasting passes on an approach that gets reframed anyway.

This connects to existing research on lens ordering: macro changes before micro, and tool
order significantly affects effectiveness.

What to look for in research: Do any frameworks address sequencing of generative vs evaluative
tools? How do adjacent formats (Amazon memos, commander's intent, design critique) sequence
the "is the whole direction right?" question relative to detail-level review?

### 3. When should Catalyst be deployed?

Current thinking: At moments when the frame itself is still a choice — brainstorm docs, PRDs,
architecture docs, key decision points. Not on every artifact, not routinely.

We can't fully predict the right deployment points yet. The pattern is: use it when the
artifact's fundamental approach is still malleable, not when you're deep in execution.

What to look for in research: Do commitment-forcing or elevation frameworks specify their own
deployment conditions? What triggers a "step back and question the whole approach" moment in
established methodologies?

## How To Process

1. Read the research results fully.
2. For each of the three questions above, pull out every relevant finding — direct evidence,
   analogous patterns, or absence of evidence (which is itself informative).
3. For each question, give me a recommendation with reasoning. "Not enough evidence to decide"
   is valid.
4. Flag anything surprising in the research that doesn't fit these three questions but matters
   for The Catalyst's design.
5. If the research suggests changes to The Catalyst, draft the specific edits — not vague
   direction, actual text changes to the prompt.
