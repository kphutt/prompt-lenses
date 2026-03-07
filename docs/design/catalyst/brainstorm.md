# The Catalyst — Initiative Brainstorm

**Author**: Karsten Huttelmaier — co-authored with Claude

A three-stage pipeline prompt that produces exactly one transformative idea for any artifact, or says nothing at all.

---

## Status

- v1 prompt exists and has been self-tested: `core/pipelines/catalyst-v1.md`
- Research landscape completed: `research/catalyst-landscape.md`
- Comprehensive design reference: `docs/design/catalyst/concept.md`
- Meta-prompt for v2 revision ready to run: `meta/catalyst-revision.md`
- Three-stage pipeline direction established (this session, not yet built)

## What The Catalyst Is

The Catalyst is NOT a lens. Lenses are evaluative — they find problems within an artifact's frame. The Catalyst is generative — it produces a new idea that doesn't exist yet. Lenses operate within the artifact's assumptions. The Catalyst questions those assumptions.

It's the only thing in the workflow that asks "should this exist in its current form?" Everything else asks "is this built well?"

See `concept.md` Parts 1-2 for full background, the v1 prompt text, and creation history.

## The Three Stages (current direction)

The original v1 is a single prompt. Research and design discussion evolved this toward a multi-stage pipeline. Current direction is three stages:

### Stage 1: Backcast (fast, frequent, cheap)

Envision the ideal version of the artifact. Measure the gap. Is it meaningful?

- No meaningful gap — stop. "No catalyst needed."
- Gap detected — pass to Stage 2.

Designed to run often, almost casually. Functions as an **inverse bloom filter** — when it says "there's a gap," that signal is high-confidence. When it says "no gap," it might be wrong (the model can't imagine a radically different version). False negatives are acceptable; false positives are not.

Following **cascade classifier theory** (Viola-Jones, medical screening): this cheap first stage should be a loose gate with high sensitivity. It catches everything real, accepts some false positives. The expensive stages clean up. See `concept.md` Part 5 for full theory.

### Stage 2: Diagnose (only when Stage 1 finds a gap)

Classifies the gap. This step gets dedicated attention because misdiagnosis is the most expensive error in the pipeline:

- **Structural** — The ideal does the same thing differently. Direction is right, organization is wrong. Fix = reorganize what exists.
- **Framing** — The ideal IS a different thing. Purpose or premise is wrong. Fix = rethink what it's trying to be. This is where the biggest wins live.
- **Both** — Structural AND framing issues can coexist. When both are present, framing typically takes priority (no point restructuring something aimed at the wrong goal).

Gap type reveals itself naturally through backcasting — if the ideal version the model envisions has the same purpose but different structure, that's structural. If it has a different purpose, that's framing. See `concept.md` Part 6 for full taxonomy and examples.

### Stage 3: The One Idea (informed by diagnosis)

Produces exactly one transformative change, constrained by the diagnosis:

- If structural — reorganize, resequence, restructure
- If framing — redefine purpose, shift thesis, change audience
- If both — address the dominant gap, acknowledge the other
- Or: "I don't have one." Honest abstention.

**Runner-up ideas are always presented.** Not for the user — for the model. Articulating what it didn't pick forces genuine discrimination and makes the winner sharper. The act of explicit comparison improves selection quality (multi-agent debate research).

**Adversarial counterargument.** The model presents the strongest argument against its own recommendation, then explains why it still holds. One stress test vs three rejected alternatives = lower cognitive load, higher quality. See `concept.md` Part 3 for the cognitive load analysis.

## Key Design Decisions

1. **Pipeline, not retry.** Each stage operates on the previous stage's output, not the original input.
2. **Catalyst runs before lenses.** It's the most macro tool — questions the whole approach. Lenses clean up within the chosen frame. Macro before micro.
3. **Framing is the unique value.** Structural insights are useful but lenses can also find those. Only the Catalyst questions premises. It should bias toward framing insights.
4. **Honest abstention is a positive outcome.** Not just permitted — valued. RLHF works against this, so it needs structural enforcement.
5. **Asymmetric error tolerance.** False negatives (missed moonshots) are far more expensive than false positives (wasted Stage 2 runs). Design accordingly.
6. **Runner-ups sharpen the winner.** They exist as a forcing function for better selection, not as output for the user.

See `concept.md` Part 14 for the full indexed list of 15 key insights.

## Proposed Deliverables

### 1. Core pipeline prompt: `core/pipelines/catalyst.md`

The model-agnostic, platform-independent three-stage pipeline. Replaces or succeeds `catalyst-v1.md`. This is a new category in prompt-lenses — pipelines alongside lenses.

### 2. Claude Code skill: `ai-toolkit/skills/catalyst/SKILL.md`

Thin operational wrapper that loads the pipeline and makes it invocable as `/catalyst` in Claude Code. Same pattern as `platforms/claude/SKILL.md` consuming lenses.

## Related Concepts

- **Premise Checker lens** — Lightweight lens (not a pipeline) that only asks "does this artifact's stated goal match the actual problem?" Could complement the Catalyst by flagging framing issues during routine review. Undesigned. See `concept.md` Part 10.4.
- **Three new lens candidates** from the Catalyst creation session: Bug Finder, Smooth Handoff, Toil Detector. See `concept.md` Part 10.3.

## Open Questions

- [ ] Three stages vs two stages vs one — the meta-prompt (`meta/catalyst-revision.md`) is designed for one-vs-two. Three-stage is the latest thinking but untested. Run the meta-prompt first, then iterate to three?
- [ ] Should Stage 2 always produce a single dominant diagnosis, or present both structural and framing with relative weights?
- [ ] Does Stage 3 always follow Stage 2, or can the diagnosis alone be the valuable output?
- [ ] Should the pipeline include confidence separation (assess confidence before generating the idea)?
- [ ] Should there be a safe-pick detector within Stage 3? ("Is this the most impactful idea or the safest?")
- [ ] Output format: commander's intent style (end-state description), adversarial counterargument, or both?
- [ ] How does `/catalyst` interact with other ai-toolkit skills?
- [ ] How does the three-stage pipeline relate to the lens synthesis step ("the one change that would improve this artifact the most")?
- [ ] Automation potential — Step 1 as a cheap screen on Google Drive docs, git hooks, etc. See `concept.md` Part 8.

## File Index

| File | Location | Purpose |
|------|----------|---------|
| v1 prompt | `core/pipelines/catalyst-v1.md` | The current operational prompt (77 lines) |
| Concept document | `docs/design/catalyst/concept.md` | Comprehensive design reference (all parts) |
| This file | `docs/design/catalyst/brainstorm.md` | Working status doc and decision log |
| Meta-prompt for v2 | `meta/catalyst-revision.md` | Ready to run — produces revised prompt |
| Research results | `research/catalyst-landscape.md` | Raw research across 6 categories |
| Research survey prompt | `research/prompts/research-prompt-catalyst.md` | The prompt that produced the research |
| Research analysis prompt | `research/prompts/process-catalyst-research.md` | Superseded by meta-prompt |
