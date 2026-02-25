You are creating a living plan document for a project called "Lenses" — a personal library of
high-quality, model-agnostic prompts for reviewing code and documents through distinct
cognitive perspectives.

This document will be updated as the project evolves. Its job is to be the single source of
truth for: what we're building, why, what's been done, what's next, and how the pieces connect.

## What to capture

### 1. The Vision (2-3 sentences)
What this project is and why it matters. The core bet: that investing heavily in prompt quality
produces compounding returns over years, across every AI platform.

### 2. Architecture Diagram
Create a Mermaid diagram (or clear ASCII art) showing:
- The prompt chain: how meta-prompts produce rosters, rosters feed into lens-crafting prompts,
  lens-crafting prompts produce the actual lenses
- The file structure: core/ (mandatory + standard lenses), meta/ (the factory), platforms/
  (thin wrappers)
- The runtime flow: user says /codelens → platform wrapper routes → loads mandatory lenses +
  standard lenses → applies each → synthesizes

### 3. The Pipeline — All Steps In Order
Number every step. For each step, include:
- **What**: One sentence describing the deliverable
- **Status**: Not started / In progress / Done / Needs revision
- **Depends on**: Which step(s) must complete first
- **Output**: The specific file(s) or artifact(s) this step produces

Here are the steps discussed so far (capture all of these, and flag if any are missing):

**Infrastructure**
- Set up the GitHub repo with the agreed file structure
- Create the README for the repo

**Research (Project 1)**
- Run the landscape survey: prompt libraries, review frameworks, meta-prompting systems,
  AI code review tools, writing/editing frameworks
- Output: research findings document

**Learn (Project 2)**
- Analyze research findings and extract concrete takeaways
- Identify techniques, structures, or specific prompts to incorporate
- Output: lessons document with specific changes to make

**Decide (Project 3)**
- Finalize the mandatory lens roster for code
- Finalize the mandatory lens roster for docs
- Decide if any additional mandatory lenses beyond the current 5 are needed
- Output: two roster files (code and doc) — just names + brief descriptions

**Build (Project 4)**
- For each mandatory lens: run it through the full meta-prompt chain
  (roster → lens-quality prompt → crafted lens)
- Build each mandatory lens as its own .md file, one at a time, with human review
- Output: the mandatory/ folder fully populated

**Standard Lenses**
- Evaluate the existing 8 code lenses and 7 doc lenses against research findings
- Revise, cut, or add standard lenses as needed
- Output: the standard/ folder populated

**Platform Wrappers**
- Build the Claude skill wrapper
- Build the Gemini Gem wrapper (or equivalent)
- Build the generic copy-paste template
- Optional: build assemble.py to auto-generate wrappers from core/

**Meta-Prompt Maintenance**
- The meta-prompts (roster designers, lens quality checker, lens selection for custom types)
  live in meta/ and are the factory for producing new lenses
- These may need updating based on research findings

### 4. Current State of Each Meta-Prompt
List every meta-prompt that exists, what it does, and its current status:
- meta-prompt-code-roster.md — designs the code lens lineup
- meta-prompt-doc-roster.md — designs the doc lens lineup
- meta-prompt-lens-selection.md — designs custom lens sets for novel artifact types
- meta-prompt.md — ensures individual lens quality (6 tests)
- research-prompt-project1.md — the research survey prompt

### 5. Design Decisions Made
Capture every decision we've made so far, so we don't re-debate them:
- Lenses are cognitive modes, not checklists
- Each lens gets its own .md file (not grouped)
- Mandatory lenses are split into -code.md and -doc.md variants
- Core lenses are model-agnostic; platform-specific stuff is in wrappers
- 5 mandatory lenses currently agreed: Security, Privacy, Testability, Plain Language, Failure Modes
- Plain Language specifically emphasizes "concrete nouns and vivid verbs" (from The Economist course)
- The user typically applies ALL suggestions, not just top 3 — anti-padding is critical
- Quality over speed: no concern about lens run time or generation time

### 6. Open Questions
Things we haven't decided yet:
- Final mandatory lens count (5 is current, research may change this)
- Whether standard lenses need the same per-file treatment as mandatory
- How to handle lenses that are mandatory for code but not docs (or vice versa)
- Versioning strategy for lenses (do we track changes over time?)
- Whether to include a "depth" parameter (mandatory-only quick mode vs. full battery)
- How custom/project-specific lenses relate to the standard set
- CI/automation: should there be any automated quality checks on lenses?

### 7. Principles
The non-negotiable beliefs driving this project:
- Prompts are the product. They compound over time.
- Separate logic (core/) from interface (platforms/)
- Each lens must change HOW the model thinks, not just WHAT it checks
- Start from failure modes, not from brainstorming lens names
- Fewer, deeper lenses beat more, shallower lenses
- No padding: if a lens finds nothing, say so and move on

## Formatting guidance
- Keep it scannable. This will be referenced frequently.
- Use checkboxes for steps so progress is visible at a glance.
- The Mermaid diagram should be simple enough to understand in 10 seconds.
- Flag dependencies clearly — some steps can run in parallel, some can't.
- Mark the critical path (the sequence of steps that determines total timeline).
