You are designing the **lens template** — the structural spec that every review lens in the
Lenses project will follow. This is the single most load-bearing artifact in the project.
Every mandatory lens, every standard lens, and every custom lens will be built on this
template. Get it right and everything downstream is easier. Get it wrong and we're
retrofitting 15+ files.

## Your Inputs

You have two files attached:
1. **plan.md** — The master plan. Read the Design Decisions (1-21) and Open Questions carefully.
   Every decision is a constraint on the template.
2. **prompt-anatomy-research.md** — Research on prompt structural patterns. Section 6 contains
   a proposed skeleton. Use it as a starting point, not as gospel.

## What You're Building

A single file: `core/template/lens-template.md`

This file has two audiences:
1. **The human** (Karsten) who will use it as a guide when crafting each lens
2. **The AI** that will be given the template as context when generating or evaluating lenses

It must be clear enough that either audience can follow it independently.

## The 8-Element Skeleton

From the research, every lens must have these 8 sections in this order:

1. **Identity** — Who is this lens? What perspective does it bring?
2. **Mission & Scope** — What this lens evaluates + what it explicitly does NOT evaluate
3. **Evaluation Criteria** — What to look for, organized by category
4. **Methodology** — How to think (the cognitive mode instruction — our differentiator)
5. **Output Format** — Exact shape of the desired output
6. **Examples** — Concrete input/output pairs showing the lens in action
7. **Edge Cases & Calibration** — Uncertainty, perfect artifacts, severity calibration
8. **Closing Anchor** — Restate the single most important principle

## Design Constraints (from plan.md decisions)

These are non-negotiable. The template must accommodate all of them:

- **Decision 1:** Lenses are cognitive modes, not checklists
- **Decision 6:** Plain Language emphasizes "concrete nouns and vivid verbs"
- **Decision 7:** User applies ALL suggestions — anti-padding is critical
- **Decision 12:** Every lens has confidence scoring and can abstain
- **Decision 13:** Shared components are fragments, not copy-paste
- **Decision 14:** Synthesis identifies inter-lens tradeoffs
- **Decision 15:** 8-element skeleton (listed above)
- **Decision 16:** Criteria (what to look for) and Methodology (how to think) are SEPARATE
- **Decision 17:** XML tags for section boundaries, markdown inside
- **Decision 18:** Every lens has explicit out-of-scope declaration
- **Decision 19:** Edge case handling is required, not optional
- **Decision 20:** Closing anchor restates the most important principle
- **Decision 21:** Prefer positive framing ("do X" not "don't do Y")

## Key Questions To Resolve IN the Template

These are open questions from the plan. The template must resolve them or explicitly define
how each lens should handle them:

### Criteria vs. Methodology relationship
The research says separate them. But our best lenses (like The Adversary) blend them — each
thinking instruction IS both a thing to look for and a way to think about it.

Resolve this. Options:
- **Option A:** Criteria is a structured list of WHAT to evaluate. Methodology is a paragraph
  describing the COGNITIVE MODE — how to approach the criteria. Think: criteria are the
  checklist items; methodology is the mindset you bring to them.
- **Option B:** Criteria are organized BY methodology. Each cognitive approach has its own
  cluster of things to look for underneath it.
- **Option C:** Something else you design.

Whatever you choose, justify it and make it concrete enough that someone writing a lens knows
exactly what goes in Criteria vs. what goes in Methodology.

### Fragment integration points
The template must clearly mark which parts are:
- **Lens-specific** (different for every lens — written fresh each time)
- **Fragment** (shared across all lenses — pulled from `core/fragments/`)
- **Hybrid** (has a shared base + lens-specific additions)

From the plan:
- Fragments (shared): Output Format, base Edge Cases, Closing Anchor pattern
- Lens-specific: Identity, Mission & Scope, Evaluation Criteria, Methodology
- Hybrid: Edge Cases (shared base + lens-specific additions)

### Confidence scoring
Every lens must assess its own relevance to the artifact. Where does this instruction go
in the template? Is it part of Methodology? Part of Edge Cases? Its own section? A fragment
that gets composed in?

### Sequencing metadata
Each lens has a position in the macro-to-micro sequence (structural → detail → style).
Where is this metadata stored? In the template frontmatter? In a comment? As part of Mission?

## What The Template Should Look Like

The template should be a complete, fill-in-the-blank document that shows:
1. The exact XML/markdown structure of a finished lens
2. For each section: what goes here, how long it should be, what makes it good vs. bad
3. Which sections are fragments (with clear markers like `{{fragment:output-format}}`)
4. Inline guidance comments that help the lens author make good decisions
5. A concrete example — fill in the template for ONE lens (suggest: the Security-Code lens)
   so the human can see what a completed template looks like in practice

## Quality Criteria for the Template Itself

The template is good if:
- A skilled prompter could write a new lens in 30 minutes by filling it in
- An AI given the template + a lens name + a brief description could generate a solid first draft
- Every lens built on the template automatically includes confidence scoring, anti-padding,
  edge case handling, and a closing anchor — without the author needing to remember
- The template enforces the separation of Criteria (what) from Methodology (how)
- The template prevents the anti-patterns from research: no role inflation, no kitchen-sink
  monoliths, no excessive negative instructions
- Two different lens authors using the template would produce structurally consistent lenses

## Output

Produce the complete `lens-template.md` file. It should include:

1. **Template header** — metadata fields (lens name, domain [code/doc], sequence phase
   [structural/detail/style], version)
2. **The 8 sections** — with XML structure, inline guidance, fragment markers, and length
   guidance for each
3. **Fragment reference table** — which fragments exist, what they contain, where they plug in
4. **One completed example** — the Security-Code lens fully written out on the template, so
   the human can compare the blank template to a finished product
5. **Template usage guide** — a short section at the top explaining how to use the template,
   including the process for creating a new lens

## Estimated Length

The template itself (without the example) should be ~200-400 lines. The completed example
adds another ~150-250 lines. Total: ~350-650 lines. This is a reference document, not a
prompt — it can be thorough.
