**Author**: Karsten Huttelmaier — co-authored with Claude

You are conducting a thorough landscape survey of how people are building reusable prompt
libraries, code/document review frameworks, and meta-prompting systems.

## Context

I'm building a personal library of high-quality, model-agnostic prompts organized as "lenses" —
distinct cognitive perspectives for reviewing code and documents. I've built a multi-layer
meta-prompt system: prompts that generate the roster of lenses, prompts that ensure each lens
is high quality, and the lenses themselves. The lenses live in a repo separate from any AI
platform, with thin wrappers for Claude, Gemini, etc.

I need to know what else exists in this space so I can learn from the best work, avoid
reinventing what's already been solved, and identify techniques or structures I haven't
considered.

## What I Need You To Find

### Category 1: Prompt Libraries & Collections
People or organizations who have built curated collections of reusable prompts, especially:
- GitHub repos of organized, high-quality prompts (not "awesome-prompts" lists of one-liners)
- Structured prompt libraries with categories, versioning, and quality standards
- Personal or team prompt toolkits that someone has refined over time
- Any repo or project specifically focused on CODE REVIEW or DOCUMENT REVIEW prompts

For each one found, I need:
- What it is and where to find it (URL)
- How it's organized (flat list? categorized? templated?)
- What makes it good or bad
- Whether the prompts are model-specific or model-agnostic
- Approximate quality level — are these throwaway one-liners or carefully crafted prompts?

### Category 2: Review Frameworks & Lenses
People who have built multi-perspective or multi-lens review systems, including:
- Anything that reviews code or docs through different "perspectives," "roles," "hats," or "lenses"
- Edward de Bono's Six Thinking Hats applied to technical review (or similar frameworks)
- Architecture review frameworks (like ATAM) that use multiple viewpoints
- Any AI-powered code review tools that use structured perspectives rather than just "find bugs"

For each one:
- The framework and how it structures its perspectives
- How many perspectives and what they are
- Whether it's designed for AI use or human use (or both)
- What's clever about how it's structured

### Category 3: Meta-Prompting & Prompt Engineering Systems
People who have built systems for generating, evaluating, or improving prompts, including:
- Meta-prompting research (prompts that write prompts)
- Prompt optimization frameworks (automated or manual)
- Prompt testing and evaluation approaches
- DSPy, OPRO, or other programmatic prompt optimization tools
- Anyone who has written about the craft of prompt engineering at a deep level (not introductory
  "tips and tricks" content — I want the people who are thinking about this seriously)

For each one:
- What the approach is
- Whether it's academic research, open source tooling, or practitioner writing
- Key insight or technique I should know about
- Relevance to building a lens-based review system

### Category 4: AI-Assisted Code Review Tools
Commercial or open-source tools that do AI-powered code review, including:
- How they structure their analysis (single pass? multiple perspectives? configurable?)
- Whether they allow custom review criteria or perspectives
- What their "lens" equivalent is, if any
- What they've learned about making AI review output high-quality and actionable

### Category 5: Writing & Editing Frameworks
Frameworks or systems for reviewing and improving written documents, including:
- Professional editing frameworks (developmental editing, line editing, copy editing as lenses)
- Plain language / clear writing standards (Federal Plain Language Guidelines, The Economist
  Style Guide, etc.)
- Document quality frameworks used in regulated industries
- Anything that structures document review as multiple distinct passes

## How To Conduct This Research

1. **Search broadly first.** Use varied search terms — don't just search "prompt library."
   Try: "reusable prompt collection github," "AI code review perspectives," "multi-lens review
   framework," "meta-prompting," "prompt engineering best practices 2024 2025," "structured
   AI review," "code review heuristics," "document review framework," "prompt optimization
   research," "six thinking hats AI," "AI writing review system."

2. **Go deep on the best finds.** When you find something promising, actually read it. Don't
   just skim the README. Look at the actual prompts, the actual structure, the actual quality.
   I want your assessment of whether this is genuinely good or just well-marketed.

3. **Look for the practitioners, not just the tools.** Some of the best work in this space
   is by individuals who have quietly built sophisticated prompt systems for their own use
   and written about it in blog posts or Twitter threads, not in polished repos. Find these
   people.

4. **Check recency.** This field moves fast. Something from 2023 might be outdated. Prioritize
   2024-2025 work but don't ignore older foundational work if it's still relevant.

5. **Be honest about quality.** Most prompt collections are low quality — surface-level,
   untested, not model-agnostic. I'd rather you find 5 genuinely excellent resources than
   list 30 mediocre ones. If a category has nothing good, say so.

## Output Format

For each category, provide:

1. **Top finds** — the best resources, with full details as specified above
2. **Honorable mentions** — worth knowing about but not as strong
3. **Key patterns** — what the best work in this category has in common
4. **Key gaps** — what's missing from the current landscape that we'd need to build ourselves
5. **Techniques to steal** — specific ideas, structures, or approaches we should incorporate

End with a **Synthesis** section:
- The 5-10 most important things I should look at, ranked
- The 3-5 most important techniques or ideas to incorporate into my lens system
- What nobody seems to be doing that we should be doing
- Honest assessment: are we ahead of, behind, or parallel to the state of the art?
