---
name: lens-review
description: >
  Review code or documents through multiple analytical "lenses" — distinct cognitive perspectives
  that each reveal different categories of issues. Use this skill whenever the user says /lenses,
  /codelens, /doclens, or asks to review code or documents through different perspectives/angles/lenses.
  Also trigger when the user asks for a thorough or multi-perspective review of any artifact.
  Even if the user just says "review this thoroughly" or "what's wrong with this", consider using
  lenses to structure the analysis.
---

# Lens Review

Reviews code or documents by systematically adopting different analytical perspectives ("lenses").
Each lens is a fully realized cognitive mode — not just "check for X" but a complete reorientation
of what you're looking for, what questions you're asking, and what "good" looks like.

## Commands

- `/lenses` — Auto-detect whether input is code or document, apply appropriate lens set
- `/codelens` — Apply code-specific lenses (8 lenses)
- `/doclens` — Apply document-specific lenses (7 lenses)
- `/lenses custom` — Design context-specific lenses for the artifact, then apply them
- `/lenses [name]` — Apply only a specific named lens (e.g., `/lenses adversary`)

## Reference Files

Load the appropriate file based on the command:

| Command | Read this file |
|---------|---------------|
| `/codelens` | `references/code-lenses.md` |
| `/doclens` | `references/doc-lenses.md` |
| `/lenses` (auto-detect) | Determine if code or document, then read the appropriate file above |
| `/lenses custom` | Read `meta-prompt-lens-selection.md` then `meta-prompt.md` |
| `/lenses [name]` | Read the file containing that lens (code or doc) |

## The Prompt Chain (for skill maintainers)

This skill was built with a 3-layer prompt chain. If you need to rebuild or update the lenses:

```
Layer 1: ROSTER DESIGN — "Which lenses should exist?"
├── meta-prompt-code-roster.md  → produces the list of code lenses + brief descriptions
├── meta-prompt-doc-roster.md   → produces the list of doc lenses + brief descriptions
└── meta-prompt-lens-selection.md → for custom/novel artifact types

Layer 2: INDIVIDUAL LENS QUALITY — "Is each lens actually good?"
└── meta-prompt.md → 6 quality tests (Identity, Cognition, Novelty, Chain, Anti-Padding, Concreteness)

Layer 3: THE LENSES THEMSELVES
├── references/code-lenses.md → 8 code review lenses
└── references/doc-lenses.md  → 7 document review lenses
```

To update the standard sets: run the roster meta-prompt → feed output into meta-prompt.md → write lenses.
Mandatory lenses (Security, Privacy, Testability, Plain Language) cannot be cut from any roster.

## How To Run a Lens Review

### Step 1: Load the lens definitions

Read the appropriate reference file based on the command. For `/lenses`, examine the artifact
to determine if it's code or a document, then load the corresponding lens set.

### Step 2: Apply Each Lens

For each lens, fully adopt that perspective before examining the artifact:

1. **State the lens name and its core question** — one sentence framing what you're looking for
2. **Perform the review from that perspective** — go deep, not broad. A lens that finds one real
   issue with clear reasoning is worth more than five shallow observations.
3. **Rate severity** — For each finding, mark it as 🔴 Critical, 🟡 Moderate, or 🔵 Minor
4. **Provide the specific fix or improvement** — Never just identify a problem; show the solution

Important: Do NOT water down findings. If a lens reveals nothing meaningful, say "This lens found
no significant issues" and move on. Padding with trivial observations destroys the signal.
If you can imagine someone shrugging and saying "yeah, I know" to your finding, it is not worth
reporting. Go deeper or move on.

### Step 3: Synthesize

After all lenses, provide:
- **Top 3 findings** across all lenses, ranked by impact
- **The one change that would improve this artifact the most**
- **What this artifact does well** (lenses are critical by nature; balance matters)

## Generating Custom Lenses

This skill includes two meta-prompts that work in sequence:

1. **`meta-prompt-lens-selection.md`** — Decides WHICH lenses to create (the portfolio)
2. **`meta-prompt.md`** — Ensures each individual lens is high quality (the crafting)

### When to use custom lenses

Use custom lenses when `/lenses custom` is requested, or when the artifact doesn't fit the
code/document categories well (e.g., config files, data pipelines, API specs, legal documents,
infrastructure-as-code, design mockups, SQL schemas, CI/CD configs).

### Process

**Phase 1: Design the lens set** (follow `meta-prompt-lens-selection.md`)

1. Read the artifact first — understand what it is before deciding how to review it
2. Build the failure mode inventory — enumerate stakeholders, lifecycle phases, quality
   dimensions, and non-obvious failures specific to this artifact type
3. Group failure modes into lenses by detection method (not topic)
4. Validate the set — coverage, redundancy, generic review subtraction, perspective diversity
5. Target 4-6 custom lenses. Never exceed 8.
6. Reuse core lenses where they fit — don't reinvent what already exists.

**Phase 2: Craft each lens** (follow `meta-prompt.md`)

Each custom lens must pass all six quality tests:
- **Identity Test**: Character with a worldview, not just a topic area
- **Cognition Test**: Thinking instructions, not checklists
- **Novelty Test**: Produces findings a generic review would miss
- **Chain Test**: Connects observations into compound findings
- **Anti-Padding Test**: Discourages shallow or obvious findings
- **Concreteness Test**: Every sub-point includes a specific example

## Design Rationale for the Core Lens Sets

**Mandatory lenses (always present in both sets):**
Security, Privacy, Testability, Plain Language & Readability. These four concerns are universal
enough that no code or document should be reviewed without them. They may be standalone lenses
or folded into a lens whose cognitive mode naturally encompasses them.

**Code lenses (8) — coverage by lifecycle phase:**
- Creation/design: Deleter (is this worth building?), Specification Lawyer (does the design cohere?)
- Implementation: Flow Analyst (data correctness), Scientist (provable correctness)
- Review/onboarding: Newcomer (comprehensibility)
- Operation: Operator (incident response), Adversary (security under attack)
- Maintenance/evolution: Time Traveler (future rot)

**Document lenses (7) — coverage by stakeholder:**
- Decision-maker: Executive (is this actionable?)
- Critical reader: Skeptic (is the reasoning sound?)
- Implementer: Implementer (can I build from this?)
- New reader: Outsider (can I understand this cold?)
- Editor/reviewer: Editor (is this concise?), Consistency Checker (does it agree with itself?)
- Dependent teams: Connector (what's missing that will block others?)

## Output Format

```
## 🗡️ THE ADVERSARY
*Core question in italics*

[findings with severity markers and specific fixes]

---

## 👶 THE NEWCOMER
...
```

End with the synthesis section.

## Important Principles

1. **Depth over breadth.** One well-reasoned finding per lens beats five surface-level observations.
2. **No padding.** If a lens reveals nothing, say so and move on. Don't manufacture issues.
3. **Show the fix.** Every finding must include a concrete improvement, not just a complaint.
4. **Be direct.** "This will break in production when X happens" not "It might be worth considering
   whether the approach to X could potentially be improved."
5. **Respect what's good.** The synthesis section should genuinely acknowledge strengths.
