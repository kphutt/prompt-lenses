# Prompt Anatomy: Structural Patterns of Excellent Prompts

**Author**: Karsten Huttelmaier — co-authored with Claude
**Date**: February 2026

---

## Section 1: Structural Patterns (The Core Finding)

After analyzing leaked production system prompts (Cursor, Claude Code, v0, Devin, Bolt), academic research on prompt formatting and ordering, Anthropic/OpenAI/Google prompting guides, and practitioner analyses, the following structural elements emerge as convergent across sources. They are listed in the order they most commonly appear.

### 1.1 Identity & Role Declaration
**What it is:** A concise statement establishing who the model is, what it does, and the operational context. Typically 2–5 sentences.

**Why it works:** Role framing narrows the model's probability space immediately, biasing token generation toward domain-appropriate vocabulary and reasoning patterns. Anthropic's own docs note that models "mirror your tone and style" and that role-setting helps the model "understand the boundaries of the task." The GPT-4.1 Prompting Guide similarly recommends framing the model as an agent with "well-defined responsibilities." Every leaked production prompt opens with identity.

**How it's formatted:** Usually plain text or a short paragraph. In Cursor: `"You are an AI coding assistant, powered by GPT-4.1. You operate in Cursor."` In Claude Code: `"You are Claude, an AI assistant made by Anthropic."` In v0: `"v0 responds using the MDX format..."` The identity is tight — no lengthy backstory.

**Universal or context-dependent:** Universal. Every production prompt examined starts with identity. However, Anthropic's latest guidance (late 2025) suggests that for modern models, being explicit about the *perspective* you want may be more effective than ornate role-playing: "Analyze this portfolio focusing on risk tolerance" outperforms "You are a world-renowned financial expert."

---

### 1.2 Behavioral Constraints & Ground Rules
**What it is:** A set of high-level behavioral rules — what the model must always do, what it must never do, and how it should handle ambiguity. This is the "constitution" of the prompt.

**Why it works:** Constraints function as invariants (a concept you'll appreciate, Karsten). They create hard boundaries that prevent the model from drifting across a wide conversation. The Cursor prompt includes rules like "never lie or make things up," "bias towards not asking the user for help," and "generated code can be run immediately." These are credited with being core to Cursor's $10B valuation — they force the model to produce *complete, runnable solutions* rather than partial sketches.

**How it's formatted:** Almost universally as a bulleted or numbered list, often inside XML tags (`<rules>`, `<guidelines>`, `<instructions>`) or under markdown headers (`# Instructions`, `## Rules`). Key constraints are often in ALL CAPS for emphasis. Cursor's 2025 prompt: `"NEVER generate an extremely long hash or any non-textual code."` OpenAI's GPT-4.1 guide notes that the model is "highly steerable and responsive to well-specified prompts" and that "a single sentence firmly and unequivocally clarifying your desired behavior is almost always sufficient."

**Universal or context-dependent:** Universal in structure, context-dependent in content. Every production prompt has this section. The *specific* rules are domain-specific.

---

### 1.3 Context Injection / Domain Knowledge
**What it is:** The long-form data the model needs to do its job — documents, codebase state, tool definitions, environment details. This is the "grounding data" section.

**Why it works:** This is where the "Lost in the Middle" research (Liu et al., 2024, TACL) becomes directly actionable. The Stanford research demonstrated a U-shaped performance curve: LLMs attend most strongly to information at the *beginning* and *end* of the context, with performance degrading by 30%+ for information positioned in the middle. Anthropic's own documentation explicitly recommends: "Put longform data at the top of your prompt, above your query, instructions, and examples. Queries at the end can improve response quality by up to 30%."

**How it's formatted:** In production prompts, context is wrapped in XML tags for clear delineation: `<codebase_context>`, `<document>`, `<user_uploaded_content>`. Cursor injects file state, linter errors, and edit history in tagged blocks. Claude Code uses `<CLAUDE.md>` content and git status. v0 wraps domain knowledge in nested XML sections. The key principle is *separation*: context is clearly fenced off from instructions.

**Universal or context-dependent:** Universal pattern (separate context from instructions). The positioning is important: place it early if long, or use XML tags to create clear boundaries regardless of position.

---

### 1.4 Detailed Task Instructions & Workflow
**What it is:** The specific, step-by-step operational instructions for how to carry out the task. This includes decision trees, conditional logic, and multi-step workflows.

**Why it works:** Specificity drives quality. The research paper "Does Prompt Formatting Have Any Impact on LLM Performance?" (Rungta et al., 2024) found that GPT-3.5-turbo's performance varied by up to 40% depending on the prompt template — and the key differentiator was structural clarity, not cleverness. The GPT-5 prompting guide reports that Cursor found "structured, scoped prompts yield the most reliable results" and that using structured XML specs like `<instruction_spec>` improved instruction adherence.

**How it's formatted:** This is where production prompts get architecturally sophisticated. Cursor 2025 uses nested tagged sections:
```
<tool_usage_policy>
  When to use semantic search vs. grep...
</tool_usage_policy>
<code_style>
  Formatting rules for generated code...
</code_style>
```
Claude Code organizes by concern: task management, tool usage policy, code references, safety, each in distinct sections. v0 uses deeply nested markdown with XML hybrid for different code block types. The pattern is: *group by concern, not by action*.

**Universal or context-dependent:** Universal pattern. The grouping strategy is consistent: organize instructions by *topic/concern*, not sequentially by "step 1, step 2."

---

### 1.5 Output Format Specification
**What it is:** Explicit instructions for what the response should look like — format, length, structure, tone.

**Why it works:** Output format specs reduce ambiguity dramatically. Multiple practitioner sources converge on this: Anthropic recommends prefilling response skeletons (starting a JSON block for the model to complete). OpenAI's guide recommends using "delimiters for clarity" including "markdown, XML tags, and section titles." The research shows that structured output enforcement (JSON or XML) "limits hallucination and dramatically improves parsing reliability."

**How it's formatted:** Often as a subsection with explicit examples. v0's prompt specifies exact code block syntax: ` ```tsx project="..." file="..." type="react" ` `. Cursor specifies heading hierarchy: "Use '###' headings and '##' headings. Never use '#' headings." Claude Code specifies that code references should use `file_path:line_number` format. The pattern is: show the *exact shape* of the desired output.

**Universal or context-dependent:** Universal. Even simple prompts benefit from output spec. Production prompts are extraordinarily specific here.

---

### 1.6 Examples (Few-Shot)
**What it is:** Concrete input/output pairs that demonstrate the desired behavior.

**Why it works:** Few-shot examples remain one of the most reliable techniques across all research. Brown et al. (2020) established this; it remains true. Anthropic's docs note that "examples show rather than tell, clarifying subtle requirements that are difficult to express through description alone." The critical nuance from Anthropic's 2025 guidance: "Claude 4.x and similar advanced models pay very close attention to details in examples. Ensure your examples align with the behaviors you want to encourage and minimize any patterns you want to avoid."

**How it's formatted:** In production prompts, examples are wrapped in `<example>` tags, often with `<input>` and `<output>` subtags. Cursor includes concrete tool-use examples. The GPT-4.1 guide provides a full customer-service agent example that "demonstrates precise behavior that incorporates all prior rules." The ratio of instruction to example in production prompts is roughly 4:1 to 6:1 — examples are concentrated, not dominant.

**Universal or context-dependent:** Universal technique, but the *quantity* depends on task complexity. Simple classification: 2–3 examples. Complex multi-step workflows: 1–2 detailed examples showing the full flow. More examples isn't always better — quality and relevance matter more.

---

### 1.7 Edge Cases, Error Handling & Anti-Behavior
**What it is:** Explicit handling of what to do when things go wrong, when the model is uncertain, or when the user asks for something outside scope.

**Why it works:** This is the "defensive programming" of prompt engineering. Production prompts invest heavily here because these are the cases that cause real-world failures. Cursor: "DO NOT loop more than 3 times on fixing linter errors on the same file." Claude Code: "NEVER propose changes to code you haven't read." The Bolt prompt is described as containing "extremely detailed handling of errors they likely faced in the past testing the product" — and this is credited as key to their $50M ARR in 5 months.

**How it's formatted:** Usually as "Important Notes" or `<important>` tagged sections, often with ALL CAPS emphasis. Positioned *after* the main instructions but *before* the end of the prompt. The pattern is: describe the failure mode, then describe the correct recovery behavior.

**Universal or context-dependent:** Universal in production-grade prompts. Often absent in amateur prompts — and this absence is the #1 differentiator between amateur and professional prompt engineering.

---

### 1.8 Closing Anchor / Final Instruction
**What it is:** A brief restatement of the most critical instruction or behavioral constraint, placed at the very end of the prompt.

**Why it works:** The "Lost in the Middle" research explains this directly: LLMs exhibit a U-shaped attention curve favoring the beginning and end. Placing the most critical instruction both at the start (in identity/constraints) and at the end (as a closing anchor) exploits both attention peaks. Anthropic's docs confirm: "Queries at the end can improve response quality by up to 30%." Multiple production prompts use this technique — Claude's system prompt repeats critical behavioral instructions at the end.

**How it's formatted:** A short paragraph or bulleted list. Often phrased differently from the opening constraint but conveying the same priority. Sometimes flagged with "CRITICAL:" or "Remember:".

**Universal or context-dependent:** Universal, and under-used. This is one of the highest-ROI structural changes you can make to any prompt.

---

## Section 2: Anatomy of the 3 Best Prompts Found

### 2.1 Cursor Agent Prompt 2.0 (GPT-4.1 version)

**Structural Breakdown:**
1. **Identity** (2 sentences): Role, tool, context
2. **Agentic behavior mandate** (1 paragraph): "You are an agent — please keep going until the user's query is completely resolved"
3. **Information gathering policy** (1 section): THOROUGH, TRACE, EXPLORE — with specific search strategy guidance
4. **Behavioral constraints** (numbered list): Never generate hashes, linter error loop limit, tool call validation
5. **Code style** (`<code_style>` tags): Indentation, formatting, line numbers as metadata
6. **Output formatting** (bulleted rules): Heading hierarchy, bold markdown, bullet structure
7. **Tool usage policy** (tagged section): When to use which tool, with decision tree
8. **Example tool calls**: Concrete demonstrations
9. **Edge case handling**: Error limits, when to stop and ask

**What makes it structurally excellent:** The Cursor prompt is a masterclass in *separation of concerns*. Each section handles one dimension of behavior. The agentic mandate comes immediately after identity — before any specific instructions — because it's the meta-instruction that governs *how* all other instructions are followed. The search strategy guidance is essentially teaching the model a *cognitive approach*, not just a task.

**What to steal for your lens template:** The separation of *how to think* (search strategy, information gathering) from *what to produce* (output format, code style). Also: the explicit loop/error limits that prevent runaway behavior.

---

### 2.2 v0 by Vercel (Nov 2024, ~13,500 tokens)

**Structural Breakdown:**
1. **Identity & capabilities** (brief): v0 responds using MDX, aims for clarity/efficiency
2. **Framework defaults**: Next.js App Router, React focus
3. **Code block type system** (deeply nested XML/markdown hybrid): Each block type (React, HTML, Python, Markdown) has its own rules
4. **Per-block-type instructions**: What v0 MUST, SHOULD, and CAN do within each block type
5. **Technical constraints** (extensive): CORS handling, import types, escape characters, environment variables
6. **Planning instruction**: "BEFORE creating a React Project, v0 THINKS through the correct structure, styling, images and media, formatting, frameworks and libraries, and caveats"
7. **Domain knowledge injection**: Specific technical knowledge for accurate responses
8. **User capabilities**: What users can upload, preview, deploy
9. **Environment constraints**: Vercel-specific rules (no .env files, integrations page)

**What makes it structurally excellent:** v0 is the most *schema-driven* prompt in the corpus. It essentially defines a type system for output: different code block types have different rules, and the prompt enforces this through deeply structured, per-type specifications. The "THINKS through" instruction before any project creation is a built-in chain-of-thought trigger that's contextually scoped — it's not a generic "think step by step," it's a specific planning checklist.

**What to steal for your lens template:** The idea of defining *output modes* — your lenses might produce different artifact types (code review comments, architectural analysis, security findings), and each type could have its own mini-spec within the prompt. Also: the planning trigger before execution.

---

### 2.3 Claude Code Main Agent System Prompt (v2.0)

**Structural Breakdown:**
1. **Identity** (brief): Who Claude is, made by Anthropic
2. **Task management** (section): Use TodoWrite for planning, break complex tasks into steps
3. **Tool usage policy** (section): File search → use Task tool (subagents); specific tool routing rules
4. **Code references** (section): Git status injected, file_path:line_number format
5. **Safety & confirmation** (section): Destructive operations require confirmation; never bypass safety checks
6. **Anti-overengineering** (added in v2.0): Guidelines on simplicity
7. **Agentic search** (section): How to find and synthesize information
8. **Subagent orchestration**: When to delegate vs. do directly
9. **Never-read-unread-code rule**: "NEVER propose changes to code you haven't read"

**What makes it structurally excellent:** Claude Code's prompt is architecturally modular — the main agent prompt is one layer in a multi-agent system where subagents (Plan, Explore, Task) each have their own specialized prompts. The main prompt focuses on *orchestration decisions* (when to delegate, when to do directly) rather than trying to be exhaustive about every task type. The "avoid over-engineering" section added in v2.0 is notable as a meta-instruction about the model's own tendency toward complexity.

**What to steal for your lens template:** The modular architecture pattern — a core prompt that handles routing and orchestration, with specialized sub-prompts for specific lens modes. Also: the explicit instruction to avoid over-engineering, which is relevant for any review/analysis lens.

---

## Section 3: Section Ordering Research

### What the Evidence Says

There is no single "canonical" order, but strong convergent evidence supports a general pattern:

**The Recommended Order (strongly supported):**

1. **Identity/Role** → first
2. **High-level behavioral constraints** → immediately after identity
3. **Context/data** → early-middle (for long contexts) or tagged anywhere (for short contexts)
4. **Detailed instructions** → middle
5. **Output format specification** → after instructions
6. **Examples** → after format spec (so the model sees the rules before the demonstrations)
7. **Edge cases** → late-middle
8. **Closing anchor / critical reminders** → last

**Evidence supporting this order:**

The "Lost in the Middle" finding (Liu et al., 2024) is the most robust academic evidence: LLMs exhibit a U-shaped attention curve. Place the most important framing (identity, constraints) at the very beginning, and the most important operational instruction (output format, critical reminders) at the very end.

Anthropic's AWS tutorial explicitly recommends this component order: (1) Task context, (2) Tone context, (3) Background data, (4) Detailed task description and rules. Their XML tags documentation adds: "Put longform data at the top... Queries at the end can improve response quality by up to 30%."

The GPT-4.1 Prompting Guide echoes this with its customer service example: role definition → instructions → detailed rules → examples. The GPT-5 guide introduces `<code_editing_rules>` with nested `<guiding_principles>` — layering from abstract to concrete.

**Task-type dependencies:**

For **system prompts** (like lenses): Identity → Constraints → Instructions → Format → Examples → Edge Cases → Anchor. This is the "strong" order.

For **task prompts** (one-shot user messages): Context → Task → Constraints → Format. Shorter, front-loaded.

For **reasoning/analysis tasks**: Adding a planning trigger ("Before responding, think through...") immediately before the main instruction improves quality. v0's "THINKS through" instruction is the canonical example.

---

## Section 4: Formatting and Delineation

### XML Tags vs. Markdown Headers vs. Plain Text

**The convergent finding:** XML tags are the most effective structural delimiter for Claude; markdown headers work well for GPT models; production prompts frequently use hybrids.

**XML Tags — When and Why:**

Anthropic's documentation states explicitly: "Claude was trained with XML tags in the training data." Zack Witten (Anthropic's senior prompt engineer) confirmed at AI Engineer 2024 that XML tags are Claude's preferred structural mechanism. Anthropic's training notebook clarifies: "There are no special sauce XML tags that Claude has been trained on — Claude is purposefully malleable and customizable." In other words, use *any* descriptive tag names; the format itself is what helps, not specific tag names.

Practitioner research claims a 15–20% performance improvement from switching from plain text to XML tags for Claude specifically. XML's key advantage is *nesting*: it supports hierarchical structure that flat markdown cannot express. For complex prompts with subsections, XML is superior.

**Markdown Headers — When and Why:**

GPT models respond well to markdown. The GPT-4.1 guide uses markdown headers (`# Instructions`, `## Rules`) throughout its examples. Cursor's GPT-powered prompt uses markdown for output formatting but XML for tool definitions. The key advantage of markdown is *human readability* — it's easier for prompt engineers to scan and edit.

**The Hybrid Approach (production consensus):**

Every major production prompt examined uses a hybrid:
- **XML tags** for data boundaries (wrapping context, examples, tool definitions)
- **Markdown headers** for navigational structure within instruction sections  
- **Numbered/bulleted lists** for sequential rules
- **ALL CAPS** for critical emphasis points
- **Bold markdown** for inline emphasis

This hybrid approach is the de facto standard. The GPT-5 guide reports that Cursor uses `<[instruction]_spec>` XML tags specifically because they "improved instruction adherence" and "allow them to clearly reference previous categories and sections elsewhere in their prompt."

**Model-Agnostic Recommendation:**

For a lens library targeting multiple models, XML tags for *section boundaries* with markdown for *internal structure* is the safest approach. XML works well on Claude (trained for it) and is also effective on GPT-4.1/5 (which Cursor uses). The one caveat: OpenAI's reasoning models (o-series) prefer simpler formatting — but these are unlikely to be your primary target for code review lenses.

---

## Section 5: Anti-Patterns

### 5.1 The Kitchen Sink Prompt
**The pattern:** Stuffing every possible instruction, edge case, and example into a single monolithic block with no structural separation.

**Why it fails:** Without section boundaries, instructions bleed into each other and the model loses track of which rules apply to which situations. The "Lost in the Middle" effect compounds — instructions in the middle of the blob get less attention. The Anthropic Skills architecture (launched Oct 2025) was explicitly designed to combat this: modular, routed capability bundles instead of one massive prompt.

**Evidence:** Claude Code v2.0 *removed* batch tools and shortened its prompt, trusting the model more. Shorter, structured prompts outperformed longer monolithic ones.

### 5.2 Excessive Negative Instructions
**The pattern:** Long lists of "Do NOT do X" instructions.

**Why it fails:** Anthropic's Zack Witten explicitly warned: "Telling Claude too forcefully what not to do can sometimes backfire and actually encourage that behavior through a kind of reverse psychology effect." LLMs are completion engines — mentioning a behavior (even negated) activates the associated patterns. The recommendation: "Use negative prompting sparingly and with a light touch."

**Evidence:** Practitioner consensus and Anthropic's own documentation. Use positive framing ("Do X") rather than negative framing ("Don't do Y") whenever possible. Reserve explicit negations for truly critical safety constraints.

### 5.3 Vague Role Inflation
**The pattern:** "You are the world's most brilliant, most experienced, most accomplished expert in every domain..."

**Why it fails:** Anthropic's 2025 prompting guide states directly: "'You are a helpful assistant' is often better than 'You are a world-renowned expert who only speaks in technical jargon and never makes mistakes.' Overly specific roles can limit the AI's helpfulness." Inflated roles introduce unnecessary constraint on the model's output distribution without improving quality.

**Evidence:** Anthropic documentation, corroborated by practitioner experience across sources.

### 5.4 Instructions in the System Message Only
**The pattern:** Putting all behavioral instructions in the system message and treating user messages as pure data/queries.

**Why it fails:** Witten noted that "Claude follows instructions in the human messages better than those in the system message." The system message is best used for high-level scene-setting and tool definitions; detailed operational instructions should go in user messages or be reinforced there.

**Evidence:** Anthropic's workshop guidance. This is somewhat Claude-specific — GPT models may not exhibit the same asymmetry — but it's worth noting for model-agnostic design.

### 5.5 Not Testing Across Prompt Variations
**The pattern:** Writing one prompt, testing it once, declaring victory.

**Why it fails:** The research on prompt formatting (Rungta et al., 2024) found performance variations of up to 40% just from formatting changes. Sclar et al. (2023) showed that "seemingly trivial design choices can lead to large performance gaps." Prompts are not deterministic — they need evaluation across variations, models, and edge cases.

**Evidence:** Multiple academic papers. OpenAI's guide explicitly recommends "building evals that measure the behavior of your prompts so you can monitor prompt performance as you iterate."

### 5.6 Optimizing for Clean Inputs, Ignoring Messy Reality
**The pattern:** Building prompts that work great with well-formed examples but haven't been tested with real, messy input data.

**Why it fails:** One practitioner analysis of thousands of failed implementations identified this as the #1 mistake: "Teams build prompts that work great with clean, predictable inputs but fall apart with real user data."

**Evidence:** Practitioner experience, corroborated by Bolt's success — their prompt's extensive error-handling section is credited as central to product reliability.

---

## Section 6: Recommended Template Skeleton for "Lens" Prompts

Based on the convergent evidence across production prompts, academic research, and practitioner wisdom, here is the proposed structural skeleton for your lens library.

```xml
<lens>

  <!-- SECTION 1: Identity (Required) -->
  <!-- 2-4 sentences. Who is this lens? What perspective does it bring? -->
  <!-- Evidence: Universal in all production prompts. Keep it specific but not inflated. -->
  <identity>
    You are a [specific reviewer role] analyzing [target artifact type]. 
    Your perspective focuses on [specific dimension of quality].
    You approach reviews with [key methodology/philosophy].
  </identity>

  <!-- SECTION 2: Mission & Scope (Required) -->  
  <!-- What this lens looks for, and equally important, what it ignores. -->
  <!-- Evidence: Cursor's constraints section; prevents scope creep. -->
  <mission>
    <focus>[What this lens evaluates — specific dimensions, categories]</focus>
    <out_of_scope>[What this lens explicitly does NOT evaluate]</out_of_scope>
  </mission>

  <!-- SECTION 3: Evaluation Criteria (Required) -->
  <!-- The specific things to look for, organized by category. -->
  <!-- Evidence: Production prompts group by concern, not by sequence. -->
  <criteria>
    <category name="[Category 1]">
      [Specific things to evaluate in this category]
    </category>
    <category name="[Category 2]">
      [Specific things to evaluate in this category]
    </category>
    <!-- Add categories as needed -->
  </criteria>

  <!-- SECTION 4: Methodology (Required) -->
  <!-- HOW to think, not just WHAT to produce. -->
  <!-- Evidence: v0's "THINKS through" pattern; Cursor's search strategy. -->
  <!-- This is the cognitive mode instruction. -->
  <methodology>
    Before producing findings, analyze the artifact by:
    1. [First analytical step]
    2. [Second analytical step]
    3. [Pattern/principle to apply]
    
    For each finding, assess: [severity/impact framework]
  </methodology>

  <!-- SECTION 5: Output Format (Required) -->
  <!-- Exact shape of the desired output. -->
  <!-- Evidence: Universal; output spec dramatically reduces ambiguity. -->
  <output_format>
    Structure your review as:
    
    ## Summary
    [1-2 sentence overall assessment]
    
    ## Findings
    For each finding:
    - **[Severity]**: [Brief title]
      - Location: [where in the artifact]
      - Issue: [what's wrong]
      - Recommendation: [specific fix]
      - Rationale: [why this matters]
    
    ## Verdict
    [Overall assessment with confidence level]
  </output_format>

  <!-- SECTION 6: Examples (Optional but Recommended) -->
  <!-- 1-2 concrete input/output pairs showing the lens in action. -->
  <!-- Evidence: Few-shot remains highly effective; quality over quantity. -->
  <examples>
    <example>
      <input>[Representative artifact snippet]</input>
      <analysis>[Model analysis demonstrating desired behavior]</analysis>
    </example>
  </examples>

  <!-- SECTION 7: Edge Cases & Calibration (Required for production) -->
  <!-- What to do when uncertain, when artifact is perfect, when it's terrible. -->
  <!-- Evidence: #1 differentiator between amateur and production prompts. -->
  <edge_cases>
    - If the artifact is too short/incomplete to evaluate: [behavior]
    - If no issues are found: [behavior — don't manufacture problems]
    - If a finding is uncertain: [behavior — flag confidence level]
    - Severity calibration: [what constitutes critical vs. minor]
  </edge_cases>

  <!-- SECTION 8: Closing Anchor (Required) -->
  <!-- Restate the single most important behavioral constraint. -->
  <!-- Evidence: "Lost in the Middle" — end position gets high attention. -->
  <anchor>
    Remember: [Single most important principle for this lens]. 
    Prioritize [key quality] over [common failure mode].
  </anchor>

</lens>
```

### Rationale for Each Decision

| Decision | Evidence Strength | Notes |
|----------|------------------|-------|
| XML tags for section boundaries | **Strong** — Anthropic training data, production consensus, GPT-5/Cursor validation | Model-agnostic safe choice |
| Identity first | **Strong** — Universal in production prompts | Keep it 2-4 sentences |
| Mission/scope as separate section | **Strong** — Cursor's constraint pattern | Prevents scope creep in reviews |
| Methodology ("how to think") | **Moderate** — v0's THINKS pattern, Cursor's search strategy | Informed judgment: this is what separates a *lens* from a generic prompt |
| Output format with exact shape | **Strong** — Universal recommendation | Show the structure, not just describe it |
| Examples after format spec | **Moderate** — Anthropic's ordering recommendation | Model sees rules before demonstrations |
| Edge cases before closing | **Strong** — Production prompt pattern | This is where production quality lives |
| Closing anchor | **Strong** — "Lost in the Middle" research, Anthropic 30% improvement claim | Highest-ROI structural addition |

### Estimated Length Range

Based on production prompt analysis:

- **Minimal viable lens:** ~500–800 tokens (identity + mission + criteria + output format + anchor)
- **Standard lens:** ~1,000–2,000 tokens (all sections, 1 example)
- **Complex lens:** ~2,000–4,000 tokens (all sections, 2 examples, extensive criteria)

For context: Cursor's agent prompt is ~3,000–4,000 tokens. v0's full prompt is ~13,500 tokens. Claude Code's main agent prompt is ~5,000+ tokens. Your lenses will be shorter because they're single-purpose, not general-purpose agent prompts.

### What's Required vs. Optional

| Section | Status | Rationale |
|---------|--------|-----------|
| Identity | Required | Universal pattern, establishes perspective |
| Mission & Scope | Required | Prevents scope creep — critical for focused review lenses |
| Evaluation Criteria | Required | The actual content of the lens |
| Methodology | Required | The differentiator: teaches the model *how* to think for this lens |
| Output Format | Required | Consistency across runs and models |
| Examples | Recommended | Include at least 1 for any lens with non-obvious output expectations |
| Edge Cases | Required for production | The difference between demo-quality and production-quality |
| Closing Anchor | Required | High-ROI, low-cost structural element |

---

## Appendix: Key Sources

**Leaked Production Prompts:**
- Cursor Agent Prompt 2.0 (GPT-4.1) — x1xhlol/system-prompts-and-models-of-ai-tools
- v0 by Vercel (Nov 2024) — 2-fly-4-ai/V0-system-prompt
- Claude Code system prompts — Piebald-AI/claude-code-system-prompts
- jujumilk3/leaked-system-prompts collection

**Academic Research:**
- Liu et al. (2024), "Lost in the Middle: How Language Models Use Long Contexts" — TACL 12:157–173
- Rungta et al. (2024), "Does Prompt Formatting Have Any Impact on LLM Performance?" — arXiv:2411.10541
- Sclar et al. (2023), minor formatting changes → large performance gaps
- He et al. (2024), "Position Engineering: Boosting LLMs through Positional Information Manipulation"

**Provider Guides:**
- Anthropic: "Use XML tags to structure your prompts" — platform.claude.com
- Anthropic: "Prompting best practices" (2025) — platform.claude.com  
- OpenAI: "GPT-4.1 Prompting Guide" — cookbook.openai.com
- OpenAI: "GPT-5 Prompting Guide" (with Cursor collaboration) — cookbook.openai.com
- OpenAI: "Reasoning Best Practices" — platform.openai.com

**Practitioner Analysis:**
- Zack Witten (Anthropic) — AI Engineer 2024 workshop, documented by PromptLayer
- Simon Willison — System prompt analysis series (simonwillison.net)
- Mikhail Shilkov — Claude Code 2.0 system prompt diff analysis
- Weaxs — Claude Code architecture reverse engineering
