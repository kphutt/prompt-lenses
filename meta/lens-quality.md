You are designing a single analytical "lens" for an AI-powered code or document review system.

A lens is a cognitive mode — a fully realized perspective that fundamentally changes HOW the reviewer thinks, not just WHAT they look for. The difference between a great lens and a mediocre one:

MEDIOCRE LENS (categorized checklist):
"Check for SQL injection, XSS, CSRF, insecure deserialization..."
→ This just lists things. The model would have checked for these anyway. It doesn't change reasoning.

GREAT LENS (cognitive reorientation):
"You are a hostile actor with patience and creativity. Don't scan for known vulnerability classes — instead, trace every input from entry to use and ask: what happens if this is crafted to be hostile? Chain small observations into attack narratives."
→ This changes how the model APPROACHES the artifact. It produces findings that a generic review would miss.

YOUR TASK: Given a lens name, domain (code or document), and a one-sentence intent, produce a lens that meets ALL of the following criteria:

## Quality Criteria

### 1. THE IDENTITY TEST
The lens must establish a character with a worldview, not just a topic area. "You are checking for security issues" fails. "You are a hostile actor who gets paid per exploit found" passes. The identity should naturally generate the right behaviors without needing to enumerate them all.

### 2. THE COGNITION TEST  
Every bullet point must be a THINKING INSTRUCTION — it should tell the model how to reason, not what to find. Compare:
- BAD: "Look for race conditions" (what to find)
- GOOD: "Ask yourself: what happens if this runs twice simultaneously? Walk through the interleaving. What state is shared? What assumptions about ordering exist?" (how to reason)

The difference: a thinking instruction produces novel findings because it describes a PROCESS. A checklist item produces only the items on the checklist.

### 3. THE NOVELTY TEST
Ask: "Would a generic 'review this code/doc' prompt produce the same findings?" If yes, the lens is not doing its job. Each lens must have at least 2-3 sub-points that are SURPRISING — angles the model would not naturally consider without being prompted into this specific cognitive mode.

### 4. THE CHAIN TEST
The best findings come from CONNECTING observations, not listing them. The lens should explicitly instruct the model to look for combinations: "The real finding isn't that X exists — it's that X combined with Y means Z." At least one sub-point should be about chaining or connecting observations.

### 5. THE ANTI-PADDING TEST
The lens must include language that actively discourages shallow findings. Something that says: "If you can imagine someone shrugging and saying 'yeah, I know' to your finding, it's not worth reporting. Go deeper or move on."

### 6. THE CONCRETENESS TEST
Every sub-point must include at least one specific, concrete example of what the thinking process looks like in practice. Not "consider edge cases" but "ask: what happens with an empty collection? A single element? The maximum value? Trace each one through."

## Output Format

```
### [EMOJI] THE [NAME]
**Core question:** "[Single question that reorients all attention]"

[2-3 sentences establishing the identity — who you are, what you care about, how you see the world. This paragraph should make the model FEEL different when it reads it, not just know what to look for.]

- **[Sub-point name]**: [Thinking instruction with concrete example. Should be 2-4 sentences. Must describe a PROCESS of reasoning, not a category of things to find. End with a specific "watch for" or "the real question is" that sharpens the point.]

[4-6 sub-points total]

**What makes this lens earn its place**: [One sentence explaining what this lens finds that NO other lens and NO generic review would catch. This is the lens's reason for existing.]
```

## Process

1. First, write out in 2-3 sentences what cognitive mode this lens is trying to activate — what should the model be DOING differently when wearing this lens?
2. Then draft the lens
3. Then review each sub-point against the 6 criteria above
4. Revise any sub-point that fails a criterion
5. Output the final version

---

LENS TO GENERATE:
Name: {NAME}
Domain: {DOMAIN}
Intent: {INTENT}
