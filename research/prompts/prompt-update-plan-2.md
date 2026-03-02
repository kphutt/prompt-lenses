**Author**: Karsten Huttelmaier — co-authored with Claude

You are updating the master plan document for the Lenses project. Phase 2.1 (Design the lens
template) has been completed. Update the plan to reflect this.

## Your Inputs

You have two files attached:
1. **plan.md** — The current master plan
2. **lens-template.md** — The completed lens template (Phase 2.1 deliverable)

## What To Update

### 1. Mark Phase 2.1 as Done

Change the checkbox and status for step 2.1 to DONE. Note the output file:
`core/template/lens-template.md`

### 2. Capture Key Decisions Resolved by the Template

The template resolved several open questions. Move these from Open Questions to Design
Decisions:

**Decision 22:** Criteria vs. Methodology uses Option A — Criteria is WHAT (observable things
to look for, grouped by category), Methodology is HOW (cognitive steps, analytical process).
Validated by the "swap test": could you change the Methodology and keep the same Criteria?
If yes, they're properly separated.

**Decision 23:** Confidence scoring lives in the output-format fragment. Two levels:
per-finding confidence (high/medium/low) and overall lens relevance (0.0-1.0). Abstention
threshold: relevance < 0.3 produces a one-line abstention instead of a full report.

**Decision 24:** Sequencing metadata is YAML front-matter with `sequence_phase` (structural /
analytical / detail) and `sequence_position` (integer for fine ordering within phase).

**Decision 25:** Fragment composition is inline assembly — at build time, every
`{{fragment:name}}` marker is replaced with the literal contents of the fragment file. The
assembled lens is self-contained with no runtime references.

### 3. Update Phase 2.2 (Fragment Design) With Specifics

The template defined exactly which fragments are needed and what each contains. Update step
2.2 to list the 5 specific fragments to build:

1. **output-format.md** — Finding structure (severity/title/location/issue/recommendation),
   severity scale (critical/major/minor/note), "show the fix" requirement, confidence scoring
   (per-finding + overall relevance), anti-padding instruction, abstention format
2. **edge-cases.md** — Base edge-case handling: artifact too short/incomplete, no issues found
   (abstain gracefully), uncertain findings (flag confidence), general severity calibration
3. **anti-padding.md** — May be inlined into output-format rather than standalone. Core
   instruction: "Report only findings where a reasonable practitioner would take action."
4. **confidence-scoring.md** — May be inlined into output-format. Per-finding confidence
   levels, overall lens relevance score, abstention threshold and format.
5. **synthesis.md** — Used by platform wrapper, not individual lenses. Cross-lens summary:
   top 3 findings, inter-lens tradeoffs, "what's actually good" section.

Note: fragments 2-4 may consolidate. The template suggests anti-padding and confidence-scoring
could be inlined into output-format rather than existing as separate files. This decision
should be made during Phase 2.2.

### 4. Remove Resolved Open Questions

These open questions were resolved by the template and should be removed (they're now design
decisions):

- "How exactly do Criteria and Methodology sections relate in practice?" → Decision 22
- "How fragments are composed at runtime — inline assembly vs. reference loading?" → Decision 25

### 5. Add New Open Questions

From the template work, these new questions emerged:

- Should anti-padding and confidence-scoring be standalone fragments or inlined into
  output-format? (Decide during Phase 2.2)
- The template specifies 1,000-2,000 tokens for standard lenses, up to 4,000 for complex.
  Do the fragments add significantly to this budget? Need to measure once fragments exist.
- The Quality Checklist in the template (Section D) — should this be extracted into a
  standalone file that the lens-quality meta-prompt references?

### 6. Update the Meta-Prompts Table

Update the status of `meta/template-design.md` — this meta-prompt was never created as a
standalone file because the template was designed directly. Note this: "Skipped — template
was designed directly from research inputs rather than via meta-prompt."

### 7. Update the File Structure

Add the template to the file structure:
```
core/
├── template/
│   └── lens-template.md       ← DONE (Phase 2.1)
```

### 8. Note Impact on Downstream Phases

Add a brief note to Phase 4 (Build Mandatory Lenses) that each lens should now reference
the template and quality checklist. The build process for each lens is:

1. Fill in the template (Identity, Mission, Criteria, Methodology)
2. Compose in fragments (output-format, edge-cases)
3. Add lens-specific edge cases and output requirements
4. Write 1-2 examples (one with findings, one showing abstention)
5. Write the closing anchor
6. Run the quality checklist (Section D of the template)
7. Human sign-off

## What NOT To Change

- Don't change the Vision, Principles, or Architecture diagrams
- Don't change the pipeline phase structure (0-8)
- Don't remove any existing design decisions (1-21)
- Keep the same formatting style and tone

## Output

Produce the complete, updated plan.md file with ALL existing content preserved plus the
updates above.
