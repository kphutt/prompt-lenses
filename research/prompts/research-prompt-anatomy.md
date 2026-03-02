**Author**: Karsten Huttelmaier — co-authored with Claude

You are conducting a focused research dive on **prompt anatomy** — the structural patterns
inside the best individual prompts. This is NOT a broad landscape survey. This is specifically
about: what are the structural bones of an excellent prompt, and why do certain structural
choices work better than others?

## Context

I'm building a library of high-quality, model-agnostic prompts called "lenses" for reviewing
code and documents. I need to design a **template** — a structural spec that every lens prompt
will follow. Before I design that template, I need to understand what the best prompts in the
world actually look like structurally.

I've already done a broad landscape survey. I know about DSPy, promptfoo, AI Council, Six
Thinking Hats, the professional editing stack, etc. What I DON'T have is a deep analysis of
the actual structural anatomy of excellent prompts.

## What I Need You To Find

### 1. Dissect Leaked Production System Prompts

Leaked/reverse-engineered system prompts from tools like Cursor, Claude Code, v0, Devin,
Windsurf, and others represent the actual state of the art in prompt engineering. Find and
analyze these. For each one:

- What sections does the prompt have, and in what order?
- How are sections delineated (XML tags, markdown headers, separators)?
- What comes first — identity/role, constraints, instructions, examples?
- How do they handle output format specification?
- How do they handle edge cases and error conditions?
- How long are they? What's the ratio of instruction to example?
- What structural patterns are shared across ALL of them?

I'm especially interested in:
- The XML tag patterns (what gets tagged and why)
- How they scope behavior ("do this, don't do that")
- How they handle multi-step or conditional workflows
- How they embed domain knowledge vs. reference it

### 2. Academic Research on Prompt Structure

Find any research (2023-2025) that has studied which structural elements of prompts affect
output quality. I'm looking for:

- Does section ordering matter? (role first vs. task first vs. examples first)
- Do explicit output format specifications improve quality?
- Does including "what NOT to do" help or hurt?
- What's the effect of identity/persona framing on output quality?
- Is there research on optimal prompt length or information density?
- What does the research say about structured (XML/markdown) vs. unstructured prompts?
- Any research on the "cognitive mode" approach — telling the model HOW to think vs. WHAT to produce?

### 3. Best Individual Prompts From Open Libraries

Go into the best prompt libraries (thibaultyou/prompt-library, danielrosehill's collection,
0xeb/TheBigPromptLibrary, awesome-system-prompts collections) and find the 5-10 prompts that
are structurally the most sophisticated. Not the most creative or useful — the best
*engineered*. Analyze their anatomy.

### 4. Practitioner Wisdom on Prompt Structure

Find blog posts, Twitter threads, or articles (2024-2025) from serious practitioners who have
written about prompt structure specifically. Not "10 tips for better prompts" content — I want
the people who have thought deeply about WHY certain structures work. Look for:

- Anthropic's own prompting guides and best practices
- OpenAI's prompt engineering documentation
- Google/DeepMind's prompting research
- Individual practitioners who have written substantive analyses

### 5. The Anti-Patterns

What structural choices consistently make prompts WORSE? This is just as important as knowing
what works. Look for:

- Common structural mistakes in prompts
- Patterns that seem helpful but actually degrade output
- Things that work for simple prompts but break at scale
- Structural choices that are model-specific vs. model-agnostic

## How To Conduct This Research

1. **Prioritize primary sources.** Actual prompts > writing about prompts. I want to see the
   real structural patterns, not someone's summary of them.

2. **Go deep on 5 great examples rather than skimming 20.** When you find an excellent prompt,
   actually break it apart and analyze the anatomy section by section.

3. **Compare across sources.** The most valuable finding is a structural pattern that appears
   independently in leaked production prompts AND academic research AND practitioner wisdom.
   Convergent evidence means it's real.

4. **Be specific about what works WHERE.** Some structural choices might work for system
   prompts but not task prompts. Some might work for Claude but not GPT. Flag these.

## Output Format

### Section 1: Structural Patterns (The Core Finding)

A definitive list of structural elements that the best prompts share, in the order they
typically appear. For each element:
- What it is
- Why it works (with evidence from multiple sources)
- How it's typically formatted
- Whether it's universal or context-dependent

### Section 2: Anatomy of the 3 Best Prompts Found

Pick the 3 most structurally sophisticated prompts you found (across any source). For each:
- Full structural breakdown (sections, ordering, formatting)
- What makes it structurally excellent
- What I should steal for my lens template

### Section 3: Section Ordering Research

What does the evidence say about optimal ordering of prompt sections? Is there a canonical
order that works best? Does it depend on the task type?

### Section 4: Formatting and Delineation

XML tags vs. markdown headers vs. separators vs. plain text. What works best and when?
What does the evidence say?

### Section 5: Anti-Patterns

Structural choices to avoid, with evidence for why they fail.

### Section 6: Recommended Template Skeleton

Based on everything found, propose a structural skeleton for a "lens" prompt. This is the
key deliverable — the bones that every lens will be built on. Include:
- The sections, in order
- The formatting approach
- What goes in each section
- What's required vs. optional
- Estimated length range

Be explicit about which recommendations are strongly supported by evidence vs. which are
your informed judgment calls.
