You are updating the master plan document for a project called "Lenses." Two research projects
have now been completed, and the plan needs to reflect what was learned.

## Your Inputs

You have two files:
1. **plan.md** — The current master plan (single source of truth for the project)
2. **prompt-anatomy-research.md** — Research on prompt structural patterns

## What To Update

### 1. Mark Research Complete

Phase 1 already shows the landscape survey as done. Add a new completed entry:

- **1.2** Prompt anatomy research — DONE
  - Output: `research/project2-prompt-anatomy.md`

### 2. Capture Key Findings From Prompt Anatomy Research

Add a new subsection under Phase 1 findings summarizing the structural research. Key findings
to capture:

**The 8-element skeleton** (converges across all sources):
Identity → Constraints/Scope → Context → Methodology → Output Format → Examples → Edge Cases → Closing Anchor

**Three additions our lenses were missing:**
- **Explicit out-of-scope declaration** per lens (prevents scope creep between lenses)
- **Edge cases & calibration section** (what to do when artifact is perfect, when a finding
  is uncertain, severity calibration — the #1 differentiator between amateur and production prompts)
- **Closing anchor** (restate the single most important principle at the end — exploits the
  U-shaped attention curve from "Lost in the Middle" research)

**One structural change:**
- Separate **Criteria** (what to look for) from **Methodology** (how to think about it).
  Our current lenses blend these. The research shows separating them improves clarity.

**Formatting decision:**
- XML tags for section boundaries, markdown inside. This is the de facto standard across
  Claude and GPT. Model-agnostic safe choice.

**Anti-patterns to encode in our meta-prompts:**
- No vague role inflation ("world's most brilliant expert")
- Prefer positive framing over negative ("do X" not "don't do Y")
- No kitchen-sink monolithic prompts — separation of concerns
- Edge case handling is mandatory, not optional

### 3. Update Phase 2 (Template Design)

Phase 2 is about designing the lens template. Update it to reflect that we now have a
proposed skeleton from the research. Specifically:

- Update step 2.1 (Design the lens template) to reference the 8-element skeleton
- List the 8 sections the template must include, with required/optional status:
  1. Identity (Required) — 2-4 sentences, perspective not inflation
  2. Mission & Scope (Required) — focus + explicit out_of_scope
  3. Evaluation Criteria (Required) — what to look for, grouped by category
  4. Methodology (Required) — how to think, the cognitive mode instruction (our differentiator)
  5. Output Format (Required) — exact shape of desired output
  6. Examples (Recommended) — 1-2 concrete input/output pairs
  7. Edge Cases & Calibration (Required) — uncertainty, perfect artifacts, severity calibration
  8. Closing Anchor (Required) — restate the single most important principle

- Update step 2.2 (Design shared fragments) to clarify which template sections are fragments
  (shared across all lenses) vs. lens-specific:
  - **Fragments (shared):** Output Format, Edge Cases (base version), Closing Anchor pattern
  - **Lens-specific:** Identity, Mission & Scope, Evaluation Criteria, Methodology
  - **Hybrid:** Edge Cases have a shared base + lens-specific additions

### 4. Update Design Decisions

Add new design decisions:

- **Decision 15:** Lens template follows the 8-element skeleton: Identity → Mission & Scope →
  Criteria → Methodology → Output Format → Examples → Edge Cases → Closing Anchor.
  (From research: converges across leaked production prompts, academic research, and
  practitioner wisdom)

- **Decision 16:** Criteria and Methodology are separate sections. Criteria = what to look for.
  Methodology = how to think. Our current lenses blend these; new template separates them.
  (From research: production prompts like Cursor and v0 separate "what" from "how")

- **Decision 17:** XML tags for section boundaries, markdown for internal structure. This
  hybrid is the model-agnostic standard. (From research: Anthropic trained Claude on XML;
  Cursor validated same approach on GPT-4.1/5)

- **Decision 18:** Every lens has an explicit out-of-scope declaration to prevent scope creep
  between lenses. (From research: Cursor's constraints section)

- **Decision 19:** Every lens has edge case handling: what to do when artifact is perfect,
  when findings are uncertain, severity calibration. This is required, not optional.
  (From research: #1 differentiator between amateur and production prompts)

- **Decision 20:** Closing anchor restates the single most important principle at the end of
  every lens. (From research: "Lost in the Middle" U-shaped attention, Anthropic 30% improvement)

- **Decision 21:** Prefer positive framing. "Do X" not "Don't do Y" — except for critical
  safety/scope constraints. (From research: Anthropic's Zack Witten warned negative instructions
  can backfire)

### 5. Update Open Questions

Add or update:
- How exactly do Criteria and Methodology sections relate in practice? Is Criteria a flat
  list and Methodology the thinking process that operates on them? Or are Criteria organized
  BY methodology? (This needs to be resolved during template design)
- Should examples be required or recommended? Research says recommended, but for lenses with
  non-obvious output expectations they may be critical.
- Estimated lens length: 1,000-2,000 tokens for standard lenses. Is this compatible with
  running 10+ lenses in a single review? Context window budget matters.

### 6. Update the Existing Meta-Prompts Table

Note that the existing meta-prompts (lens-quality.md, roster meta-prompts) will need updates
to check for the 8-element skeleton, not just the current 6 quality tests.

### 7. Add Research Files to the File Structure

Update the file structure to show:
```
research/
├── project1-landscape.md          ← DONE
├── project2-prompt-anatomy.md     ← DONE (NEW)
├── prompts/
│   ├── research-prompt-project1.md
│   ├── research-prompt-anatomy.md ← NEW
│   └── plan-prompt.md
```

## What NOT To Change

- Don't change the Vision, Principles, or Architecture diagrams (unless the research
  directly contradicts them — it doesn't)
- Don't change the pipeline phase structure (0-8) — just update content within phases
- Don't remove any existing content — add to it
- Keep the same formatting style and tone as the existing plan

## Output

Produce the complete, updated plan.md file. Include ALL existing content (updated where
needed) plus the new additions. Do not summarize or abbreviate existing sections.
