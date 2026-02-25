# prompt-lenses — Context Handoff

## What This Project Is

A personal library of model-agnostic prompts ("lenses") for reviewing code and documents
through distinct cognitive perspectives. Each lens is a fully realized analytical mode — not
"check for X" but a complete reorientation of how the reviewer thinks. Built on a 3-layer
prompt chain: roster meta-prompts decide which lenses exist, a quality meta-prompt validates
each lens, and the lenses themselves are standalone `.md` files built on a shared template.

## Repo Structure

```
prompt-lenses/
├── plan.md                          ← SINGLE SOURCE OF TRUTH. Read this first.
├── ROADMAP.md                       ← Prioritized backlog
├── CLAUDE.md                        ← Project conventions
├── README.md
├── core/
│   ├── template/
│   │   └── lens-template.md         ← The 8-element skeleton every lens inherits (DONE)
│   ├── fragments/                   ← Shared components composed into lenses (DONE)
│   │   ├── output-format.md        ← Finding structure, severity, confidence, anti-padding
│   │   ├── edge-cases.md           ← Base edge-case handling for all lenses
│   │   └── synthesis.md            ← Cross-lens summary (used by platform wrapper)
│   ├── mandatory/                   ← Security, Privacy, Testability, etc. (NOT YET BUILT)
│   ├── standard/
│   │   ├── code-lenses-draft.md     ← Pre-template draft of 8 code lenses (OLD FORMAT)
│   │   ├── doc-lenses-draft.md      ← Pre-template draft of 7 doc lenses (OLD FORMAT)
│   │   ├── code/                    ← Will hold individual lens files
│   │   └── doc/                     ← Will hold individual lens files
│   └── custom/
├── meta/
│   ├── roster-code.md               ← Meta-prompt: which code lenses should exist
│   ├── roster-doc.md                ← Meta-prompt: which doc lenses should exist
│   ├── lens-selection.md            ← Meta-prompt: custom lens sets for novel artifacts
│   └── lens-quality.md              ← Meta-prompt: 6 quality tests for GENERATING lenses
├── platforms/
│   └── claude/SKILL.md              ← Claude skill wrapper (STALE DRAFT — see note below)
├── research/
│   ├── project1-landscape.md        ← Landscape survey (DONE)
│   ├── project2-prompt-anatomy.md   ← Prompt structural patterns research (DONE)
│   └── prompts/                     ← The prompts that produced research + plan updates
└── scripts/                         ← Future: assemble.py for fragment composition
```

## Things That Look Broken But Aren't

Read this before proposing fixes. These were all reviewed and confirmed intentional:

**SKILL.md file paths are all wrong.** The SKILL.md references `references/code-lenses.md`,
`meta-prompt.md`, etc. — paths from before the repo was organized. This is expected. SKILL.md
is a stale draft from the initial conversation. It will be rewritten from scratch in Phase 6.1,
which depends on Phases 4 and 5 completing first. Don't fix the paths now.

**The 6 quality tests and the 10-item checklist are not competing.** They are complementary
tools for different stages:
- `meta/lens-quality.md` (6 tests: Identity, Cognition, Novelty, Chain, Anti-Padding,
  Concreteness) is a **generative meta-prompt** — it's the prompt you use to *create* a lens.
  It validates cognitive quality: does the lens change how the model thinks?
- Template Section D (10 items) is a **structural validation checklist** — it's what you run
  *after* a lens is written to verify template compliance: are Criteria and Methodology
  properly separated? Are fragments composed? Is the closing anchor consistent?
- Phase 4 uses both: generate with the 6 tests, validate with the 10-item checklist.
- Phase 8.1 plans to update the 6 tests to also check for the 8-element skeleton structure.

**The 8-element skeleton has two different sets of element names in plan.md.** The research
section says "Identity → Constraints/Scope → Context → Methodology → ..." and the Phase 2.1
section says "Identity → Mission & Scope → Evaluation Criteria → Methodology → ...". These
are the same skeleton — the generic research names were adapted to lens-specific names during
template design. The Phase 2.1 names are canonical.

**The draft lenses are a completely different format.** `code-lenses-draft.md` and
`doc-lenses-draft.md` predate the template. They have no XML tags, no Criteria/Methodology
separation, no edge cases, no YAML front-matter, no confidence scoring. They are reference
material for *what cognitive modes were identified*, not usable lenses. Phase 5 will rebuild
every standard lens from scratch on the template.

## What's Done

- **Phase 1 (Research):** Both projects complete. Key findings are in plan.md under
  "Key Findings From Landscape Research" and "Key Findings From Prompt Anatomy Research."
- **Phase 2.1 (Template):** `core/template/lens-template.md` is done. It defines the
  8-element skeleton (Identity → Mission & Scope → Criteria → Methodology → Output Format →
  Examples → Edge Cases → Closing Anchor), includes a completed Security-Code example lens,
  a quality checklist, fragment reference table, and anti-pattern guide.
- **Phase 2.2 (Fragments):** `core/fragments/` populated with 3 files: `output-format.md`,
  `edge-cases.md`, `synthesis.md`. Anti-padding and confidence-scoring were inlined into
  output-format (Design Decision #26). Inter-lens tradeoffs use simple flagging (DD #27).
  `synthesis.md` is flagged for re-validation during Phase 4.1.
- **Phase 0 (Infra):** Repo structured, README, CLAUDE.md, ROADMAP.md, git hygiene in place.

## What's Next (Critical Path)

```
Phase 3 (rosters) → Phase 4 (mandatory lenses) → Phase 5 (standard lenses) → Phase 6 (wrappers)
```

**Immediate next step: Phase 3 — Finalize mandatory lens rosters.** Notes from Phase 2.2
dogfooding to consider:
- Design mandatory lens scope boundaries as a set — each lens's `<out_of_scope>` should
  reference the other mandatory lenses by name.
- Evaluate the Connector for mandatory status.
- The Testability lens's "falsifiable check" was the highest-ROI transformation during
  dogfooding — strengthens the case for mandatory.

## Key Design Decisions (most important)

- Lenses are cognitive modes, not checklists — each changes HOW the model thinks
- Criteria (WHAT to look for) and Methodology (HOW to think) are separate sections
- Every lens has confidence scoring (0.0-1.0) and abstains below 0.3
- Fragment composition is inline assembly: `{{fragment:name}}` replaced at build time
- XML tags for section boundaries, markdown inside
- Macro-to-micro sequencing: structural lenses before detail lenses
- No padding, ever. If a lens finds nothing, it says so.

There are 27 numbered design decisions in plan.md — read them before making structural changes.

## Key Files to Read

1. `plan.md` — Everything: architecture, pipeline, decisions, open questions
2. `core/template/lens-template.md` — How lenses are structured (Section A = blank template,
   Section E = completed example, Section D = quality checklist)
3. `meta/lens-quality.md` — The 6 quality tests for *generating* lens content (complements
   the template's 10-item structural checklist in Section D — they serve different purposes)

## Lens Candidates to Evaluate

Three new lens ideas emerged from real usage. Evaluate during Phase 3:
1. **Bug Finder** (code + doc) — dedicated "find what's broken" lens
2. **Smooth Handoff** (doc, maybe code) — will the next person trip over this?
3. **Toil Detector** (doc + code) — what's manual that could be automated?

## Lens Candidates to Evaluate (Phase 3)

Three lens ideas emerged from using the project. Evaluate during roster finalization:

1. **Bug Finder** — Literally trace execution and find bugs. Different from Scientist
   (provable correctness) or Spec Lawyer (contract compliance). Code version: off-by-ones,
   null derefs, stale state, race conditions. Doc version: factual errors, broken references,
   specs that are unimplementable as written. Partially overlaps existing lenses but none
   focus on "just find what's wrong."

2. **Smooth Handoff** — Will the next person who touches this trip over something? For docs:
   navigation friction, things that look broken but aren't, missing context that causes wrong
   assumptions. For code: API ergonomics, non-obvious happy paths, interfaces that invite
   misuse. Different from Implementer (can I build from this) — this is about the *experience*
   of picking it up, not whether the content is sufficient.

3. **Toil Detector** — Manual effort that could be automated, even if it requires challenging
   assumptions about how things are currently done. For code: copy-paste patterns, manual
   steps in workflows, things done by convention that a script could enforce. For docs:
   processes described as manual that have automation paths, repeated boilerplate across
   documents. This lens should think outside the box — not just "automate what exists" but
   "should this exist at all?"

All three may have both code and doc variants. Decide during Phase 3 whether they're
standard or mandatory, and whether each needs both variants.

## Style Notes

- This is a docs/prompts project, not a code project
- Markdown files are the product — prompt quality matters more than anything
- "Concrete nouns and vivid verbs" is a guiding principle (from The Economist)
- Positive framing ("do X" not "don't do Y") except for out-of-scope declarations
