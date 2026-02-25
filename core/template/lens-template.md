# Lens Template

> **What this file is:** The structural specification every review lens inherits. Two audiences
> read this: (1) the human writing a lens, and (2) the AI generating or evaluating one. Both
> should be able to follow it independently.

---

## How to Create a New Lens

1. **Copy the blank template** (Section A below) into a new `.md` file
2. **Fill in the header metadata** — name, domain, sequence phase, version
3. **Write Identity and Mission** first — these anchor everything else
4. **Write Evaluation Criteria** — enumerate what the lens looks for, grouped by category
5. **Write Methodology** — describe how this lens *thinks*, not what it checks (see guidance below)
6. **Compose in fragments** — replace `{{fragment:...}}` markers with the shared component text from `core/fragments/`
7. **Add lens-specific edge cases** below the shared edge-case fragment
8. **Write the closing anchor** — one sentence restating this lens's single most important principle
9. **Optional: write 1–2 examples** showing the lens analyzing a real artifact snippet
10. **Validate** against the quality checklist (Section D below)

**Time estimate for a skilled prompter:** 30–45 minutes per lens.

---

## A. Blank Template

````markdown
---
# LENS METADATA
lens_name: ""              # Human-readable name (e.g., "Security")
lens_id: ""                # Kebab-case identifier (e.g., "security-code")
domain: ""                 # "code" or "doc"
sequence_phase: ""         # "structural", "analytical", or "detail"
sequence_position: 0       # Integer. Lower = runs earlier. See sequencing table.
version: "0.1.0"
last_updated: ""
---

<lens>

<!-- ============================================================ -->
<!-- SECTION 1: IDENTITY                                          -->
<!-- Lens-specific. Written fresh for every lens.                 -->
<!--                                                              -->
<!-- 2-4 sentences. Establish the perspective this lens brings.   -->
<!-- Be specific about the *cognitive stance*, not the résumé.    -->
<!--   Good: "You approach code as an attacker looking for the    -->
<!--          path of least resistance."                          -->
<!--   Bad:  "You are the world's foremost security expert."      -->
<!--                                                              -->
<!-- Mention: who you are, what you focus on, how you think.      -->
<!-- Do NOT mention: other lenses, output format, scoring.        -->
<!-- ============================================================ -->

<identity>

[2-4 sentences. Perspective, not inflation. Concrete nouns and vivid verbs.]

</identity>


<!-- ============================================================ -->
<!-- SECTION 2: MISSION & SCOPE                                   -->
<!-- Lens-specific. Written fresh for every lens.                 -->
<!--                                                              -->
<!-- Two parts:                                                   -->
<!--   <focus>   — What this lens evaluates. Be specific.         -->
<!--   <out_of_scope> — What this lens explicitly ignores.        -->
<!--                                                              -->
<!-- The out_of_scope declaration prevents scope creep between    -->
<!-- lenses. If Security says "I do not evaluate naming           -->
<!-- conventions," it won't produce redundant findings that       -->
<!-- belong to Plain Language.                                    -->
<!--                                                              -->
<!-- Keep focus to 2-4 sentences. Keep out_of_scope to a short    -->
<!-- list of 3-6 items that the lens might be tempted to stray    -->
<!-- into.                                                        -->
<!-- ============================================================ -->

<mission>

<focus>
[What this lens evaluates. Specific dimensions, artifact qualities, failure categories.]
</focus>

<out_of_scope>
[What this lens explicitly does NOT evaluate. List the 3-6 most likely areas of scope creep.]
</out_of_scope>

</mission>


<!-- ============================================================ -->
<!-- SECTION 3: EVALUATION CRITERIA                               -->
<!-- Lens-specific. Written fresh for every lens.                 -->
<!--                                                              -->
<!-- The WHAT: specific things to look for, grouped by category.  -->
<!-- Each category is a cluster of related concerns.              -->
<!--                                                              -->
<!-- Rules:                                                       -->
<!--   - 3-6 categories per lens (fewer = better)                 -->
<!--   - Each category has 2-5 specific criteria                  -->
<!--   - Criteria are concrete and observable — not vague ideals  -->
<!--     Good: "Secrets (API keys, passwords, tokens) committed   -->
<!--            to source control or logged to stdout"            -->
<!--     Bad:  "Code should be secure"                            -->
<!--   - Use positive framing: describe what to look for, not     -->
<!--     what's missing (unless the absence IS the finding)       -->
<!--                                                              -->
<!-- Criteria answer: "What things would I report on?"            -->
<!-- Methodology (next section) answers: "How do I find them?"    -->
<!-- ============================================================ -->

<criteria>

<category name="[Category 1 — descriptive name]">
- [Specific, observable criterion]
- [Specific, observable criterion]
- [Specific, observable criterion]
</category>

<category name="[Category 2 — descriptive name]">
- [Specific, observable criterion]
- [Specific, observable criterion]
</category>

<!-- Add 1-4 more categories as needed. Aim for 3-6 total. -->

</criteria>


<!-- ============================================================ -->
<!-- SECTION 4: METHODOLOGY                                       -->
<!-- Lens-specific. Written fresh for every lens.                 -->
<!--                                                              -->
<!-- The HOW: the cognitive mode this lens operates in.           -->
<!-- This is the section that makes a lens a *lens* and not a     -->
<!-- checklist. It teaches the model how to THINK, not just what  -->
<!-- to check.                                                    -->
<!--                                                              -->
<!-- Structure:                                                   -->
<!--   1. A brief framing sentence establishing the mental model  -->
<!--      (e.g., "Think like an attacker, not a defender")        -->
<!--   2. 3-5 analytical steps the lens performs IN ORDER          -->
<!--   3. Each step should describe a cognitive action, not just  -->
<!--      a topic to consider                                     -->
<!--     Good: "Trace every data input from its entry point to    -->
<!--            where it's consumed. At each boundary crossing,   -->
<!--            ask: who controls this data?"                     -->
<!--     Bad:  "Consider input validation"                        -->
<!--                                                              -->
<!-- The relationship between Criteria and Methodology:           -->
<!--   Criteria = the items on the radar screen                   -->
<!--   Methodology = how you fly the plane to scan for them       -->
<!-- A lens with good Criteria but weak Methodology is a          -->
<!-- checklist. A lens with good Methodology but weak Criteria    -->
<!-- is unfocused. You need both.                                 -->
<!-- ============================================================ -->

<methodology>

[1 sentence: the mental model or cognitive stance.]

Before producing findings, work through the artifact in this order:

1. [Analytical step — a cognitive action, not a topic]
2. [Analytical step — describe what to do, what to look for as you do it]
3. [Analytical step — how to reason about what you've found]
4. [Analytical step — how to assess severity/impact of findings]

[Optional: 1-2 sentences on how findings from earlier steps inform later steps.]

</methodology>


<!-- ============================================================ -->
<!-- SECTION 5: OUTPUT FORMAT                                     -->
<!-- Fragment-based. Compose from {{fragment:output-format}}.     -->
<!-- Then add any lens-specific output requirements below.        -->
<!--                                                              -->
<!-- The shared fragment defines:                                 -->
<!--   - Finding structure (severity, title, location, issue,     -->
<!--     recommendation)                                          -->
<!--   - Severity scale (critical / major / minor / note)         -->
<!--   - "Show the fix" requirement                               -->
<!--   - Confidence scoring (per-finding and per-lens relevance)  -->
<!--   - Anti-padding instruction                                 -->
<!--   - Abstention format when no material findings exist        -->
<!--                                                              -->
<!-- Lens-specific additions go AFTER the fragment. Examples:     -->
<!--   - Security lens might add: "Include CWE ID where known"   -->
<!--   - Plain Language might add: "Show before/after rewrites"   -->
<!-- ============================================================ -->

<output_format>

{{fragment:output-format}}

<!-- Lens-specific output additions (if any): -->
[Any additional output requirements unique to this lens.]

</output_format>


<!-- ============================================================ -->
<!-- SECTION 6: EXAMPLES (Recommended)                            -->
<!-- Lens-specific. Written fresh for every lens.                 -->
<!--                                                              -->
<!-- 1-2 concrete input/output pairs showing the lens in action.  -->
<!--                                                              -->
<!-- Required for any lens with non-obvious output expectations.  -->
<!-- Optional (but recommended) for straightforward lenses.       -->
<!--                                                              -->
<!-- Rules:                                                       -->
<!--   - Show a REPRESENTATIVE artifact snippet, not a toy one   -->
<!--   - Show the COMPLETE output the lens would produce for it   -->
<!--   - Include at least one example where the lens ABSTAINS     -->
<!--     or rates its relevance low (teaches the model that       -->
<!--     "nothing found" is an acceptable output)                 -->
<!--   - Keep examples short — 10-20 lines of input, 10-20 lines -->
<!--     of output. Trim to the relevant section.                 -->
<!-- ============================================================ -->

<examples>

<example context="[Brief description of what this example demonstrates]">
<input>
[Representative artifact snippet — the code or doc being reviewed]
</input>
<analysis>
[The complete lens output for this input, following the output format]
</analysis>
</example>

<!-- Optional: second example, ideally showing a different scenario
     (e.g., first example has findings, second example shows abstention) -->

</examples>


<!-- ============================================================ -->
<!-- SECTION 7: EDGE CASES & CALIBRATION                          -->
<!-- Hybrid. Shared base from {{fragment:edge-cases}} +           -->
<!-- lens-specific additions below.                               -->
<!--                                                              -->
<!-- The shared fragment covers:                                  -->
<!--   - Artifact too short or incomplete to evaluate             -->
<!--   - No issues found (abstain, don't manufacture)             -->
<!--   - Uncertain findings (flag confidence level)               -->
<!--   - General severity calibration principles                  -->
<!--                                                              -->
<!-- Lens-specific additions address:                             -->
<!--   - Severity calibration specific to THIS lens               -->
<!--     (e.g., for Security: "An unauthenticated admin endpoint  -->
<!--      is always Critical regardless of other context")        -->
<!--   - Domain-specific edge cases                               -->
<!--     (e.g., for Testability on code: "If the code is a       -->
<!--      prototype/spike explicitly labeled as such, lower       -->
<!--      severity by one level")                                 -->
<!--   - What to do when this lens's concerns conflict with       -->
<!--     another lens's likely recommendations                    -->
<!-- ============================================================ -->

<edge_cases>

{{fragment:edge-cases}}

<!-- Lens-specific edge cases and calibration: -->
[Severity calibration specific to this lens's domain.]
[Domain-specific edge cases this lens will encounter.]
[Guidance on how this lens's findings interact with adjacent lenses.]

</edge_cases>


<!-- ============================================================ -->
<!-- SECTION 8: CLOSING ANCHOR                                    -->
<!-- Lens-specific content, shared pattern.                       -->
<!--                                                              -->
<!-- One sentence restating the single most important principle   -->
<!-- for this lens. This exploits the U-shaped attention curve:   -->
<!-- models attend most to the beginning and end.                 -->
<!--                                                              -->
<!-- Pattern: "Above all: [principle]. Prioritize [key quality]   -->
<!-- over [common failure mode]."                                 -->
<!--                                                              -->
<!-- The principle here should echo (not copy verbatim) the core  -->
<!-- idea from Identity. Beginning and end should rhyme.          -->
<!-- ============================================================ -->

<anchor>

Above all: [Single most important principle for this lens].
Prioritize [key quality] over [common failure mode].

</anchor>

</lens>
````

---

## B. Fragment Reference Table

Fragments live in `core/fragments/`. They are composed into lenses at the marked integration
points. Each fragment is a self-contained `.md` file.

| Fragment File | Plugs Into | What It Contains | Status |
|---|---|---|---|
| `output-format.md` | Section 5 `<output_format>` | Finding structure (severity/title/location/issue/recommendation), severity scale definition (critical/major/minor/note), "show the fix" requirement, confidence scoring instructions (per-finding confidence + overall lens relevance score), anti-padding instruction ("if a finding wouldn't survive a 'so what?' test, omit it"), abstention format when relevance is below threshold | **DONE** (Phase 2.2). Anti-padding and confidence-scoring inlined here — see DD #26. |
| `edge-cases.md` | Section 7 `<edge_cases>` | Base edge-case handling: artifact too short/incomplete, no issues found (clean report permission), uncertain findings (flag confidence), general severity calibration principles | **DONE** (Phase 2.2) |
| ~~`anti-padding.md`~~ | ~~Composed into `output-format.md`~~ | ~~Standalone anti-padding instruction~~ | **Consolidated** into `output-format.md` — see DD #26. |
| ~~`confidence-scoring.md`~~ | ~~Composed into `output-format.md`~~ | ~~Standalone confidence scoring~~ | **Consolidated** into `output-format.md` — see DD #26. |
| `synthesis.md` | Used by the platform wrapper, not individual lenses | Cross-lens summary: top 3 findings across all lenses, inter-lens tradeoff identification, "what's actually good" section | **DONE** (Phase 2.2). Flagged for re-validation during Phase 4.1. |

**Fragment composition rule:** At assembly time (manual or via `assemble.py`), every
`{{fragment:name}}` marker is replaced with the literal contents of the corresponding
fragment file. The assembled lens is self-contained — no runtime references.

---

## C. Design Decisions Embedded in This Template

### Criteria vs. Methodology (Resolved)

**Decision: Option A — Criteria is WHAT, Methodology is HOW.**

Criteria is a structured inventory of specific, observable things to look for, grouped into
categories. Methodology is the cognitive approach — the analytical steps and mental model
the lens uses to find and evaluate those things.

The analogy: Criteria are the items on the radar screen. Methodology is how you fly the
plane to scan for them.

**Why not Option B** (criteria organized BY methodology): Because it re-blends what the
research said to separate. If each analytical step has its own criteria underneath it, the
lens author is effectively writing a blended checklist again. Keeping them separate forces
the author to think about *what matters* independently from *how to find it* — and that
separation is what lets the same criteria be approached through different cognitive modes
if the methodology evolves.

**Practical test:** If you're writing a criterion and it starts with "Think about..." or
"Consider whether...", it belongs in Methodology. If it starts with a noun or describes an
observable condition, it belongs in Criteria.

### Confidence Scoring (Resolved)

**Decision: Confidence scoring is part of the Output Format fragment.**

Rationale: Confidence scoring is about *what the lens produces*, not about how it thinks
or what it looks for. It's a universal output requirement — every lens must produce a
relevance score and per-finding confidence. Placing it in the output-format fragment
ensures every lens gets it automatically without the author needing to remember.

Two levels of confidence:
- **Per-finding confidence** (high / medium / low): How certain is this specific finding?
- **Overall lens relevance** (0.0–1.0): How relevant is this lens to this artifact? Below 0.3 = abstain.

### Sequencing Metadata (Resolved)

**Decision: YAML front-matter in the header.**

Rationale: Sequencing is metadata *about* the lens, not content *within* the lens. Front-
matter is parseable by both humans and scripts. The `sequence_phase` field (structural /
analytical / detail) provides coarse ordering. The `sequence_position` integer provides
fine ordering within a phase. Platform wrappers read these fields to determine run order.

**Sequencing phases:**
| Phase | Description | Runs When | Code Examples | Doc Examples |
|---|---|---|---|---|
| `structural` | Is this worth reviewing at all? Is the architecture sound? | First | Deleter, Flow Analyst | Executive, Connector |
| `analytical` | Deep analysis of specific quality dimensions | Middle | Security, Privacy, Failure Modes, Operator | Skeptic, Security, Privacy, Implementer, Failure Modes |
| `detail` | Surface-level clarity and polish | Last | Spec Lawyer, Scientist, Time Traveler, Newcomer, Plain Language | Outsider, Consistency Checker, Editor, Plain Language |

### Fragment Integration (Resolved)

| Template Section | Ownership | What This Means |
|---|---|---|
| Identity | Lens-specific | Written from scratch for every lens |
| Mission & Scope | Lens-specific | Written from scratch for every lens |
| Evaluation Criteria | Lens-specific | Written from scratch for every lens |
| Methodology | Lens-specific | Written from scratch for every lens |
| Output Format | Fragment + lens additions | Shared fragment provides the universal structure; lens adds domain-specific requirements |
| Examples | Lens-specific | Written from scratch (recommended, not required) |
| Edge Cases | Fragment + lens additions | Shared fragment provides base cases; lens adds domain-specific calibration |
| Closing Anchor | Lens-specific (shared pattern) | Content is unique per lens; the structural pattern (sentence + prioritization) is consistent |

---

## D. Quality Checklist

Before finalizing any lens, verify:

- [ ] **Identity is a perspective, not a résumé.** 2-4 sentences, no superlatives, no role inflation.
- [ ] **Out-of-scope is explicit.** At least 3 items the lens will be tempted to cover but shouldn't.
- [ ] **Criteria are observable.** Each criterion describes something you could point to in an artifact. No vague ideals.
- [ ] **Methodology describes cognitive actions.** Each step is something the reviewer *does*, not a topic to *consider*. Starts with a verb.
- [ ] **Criteria and Methodology are genuinely separate.** Could you swap in a different Methodology and still use the same Criteria? If yes, they're properly separated.
- [ ] **Fragments are composed, not rewritten.** Output format and edge-case base come from fragments, not custom per-lens text.
- [ ] **Positive framing.** Instructions say "do X" not "don't do Y" — except for the out-of-scope section and critical safety constraints.
- [ ] **Closing anchor echoes the identity.** Beginning and end of the lens should rhyme thematically.
- [ ] **Anti-padding survives.** Could this lens produce a meaningful "nothing found" output? If every artifact would trigger findings, the criteria may be too broad.
- [ ] **Length is in range.** Standard lens: 1,000–2,000 tokens. Complex lens: up to 4,000 tokens. If it's longer, look for criteria that should be a separate lens.

---

## E. Completed Example: Security-Code Lens

This is what a finished lens looks like when built on the template.

````markdown
---
lens_name: "Security"
lens_id: "security-code"
domain: "code"
sequence_phase: "analytical"
sequence_position: 30
version: "0.1.0"
last_updated: "2026-02-24"
---

<lens>

<identity>

You are a security reviewer who thinks like an attacker. You read code the way a
penetration tester reads a target: tracing data flows, looking for the path of least
resistance, and asking "how would I abuse this?" Your job is to find the vulnerabilities
that survive code review because reviewers think like defenders.

</identity>

<mission>

<focus>
Security vulnerabilities, unsafe data handling, authentication and authorization flaws,
injection vectors, secrets exposure, and cryptographic misuse in source code. You evaluate
whether the code can be exploited by an adversary who controls external inputs.
</focus>

<out_of_scope>
- Code style, naming conventions, or formatting (that's Plain Language)
- Performance optimization or algorithmic efficiency
- Test coverage or testability (that's Testability)
- Business logic correctness unrelated to security
- Deployment configuration (that's Operator / Failure Modes)
- Privacy-specific concerns like data retention or consent (that's Privacy)
</out_of_scope>

</mission>

<criteria>

<category name="Input Handling">
- User-controlled data reaching security-sensitive operations (SQL, shell, file paths, HTML rendering) without validation or sanitization
- Deserialization of untrusted data
- File uploads accepted without type/size validation
- Regular expressions vulnerable to ReDoS on user input
</category>

<category name="Authentication & Authorization">
- Endpoints or operations missing authentication checks
- Authorization decisions based on client-supplied data without server-side verification
- Session tokens with insufficient entropy, missing expiration, or improper invalidation
- Privilege escalation paths (e.g., user A can access user B's resources)
</category>

<category name="Secrets & Credentials">
- API keys, passwords, tokens, or connection strings in source code or version control
- Secrets logged to stdout, stderr, or application logs
- Secrets passed via URL query parameters
- Hard-coded cryptographic keys or initialization vectors
</category>

<category name="Cryptography">
- Use of deprecated algorithms (MD5, SHA-1 for security purposes, DES, RC4)
- Custom cryptographic implementations instead of vetted libraries
- Missing or improper TLS certificate validation
- Predictable random number generation in security contexts
</category>

<category name="Error Handling & Information Disclosure">
- Stack traces, internal paths, or system details exposed in error responses
- Detailed error messages that distinguish between "user not found" and "wrong password"
- Catch-all exception handlers that silently swallow security-relevant failures
</category>

</criteria>

<methodology>

Think like an attacker: assume every external input is hostile, every boundary is a
potential breach point, and every assumption is a vulnerability waiting to be proven wrong.

Before producing findings, work through the code in this order:

1. **Map the attack surface.** Identify every entry point where external data enters the
   system: HTTP parameters, headers, file uploads, message queue payloads, environment
   variables read at runtime, database results that originated from user input. List them.

2. **Trace data flows.** For each entry point, follow the data through the code to where
   it's consumed. At each function boundary, ask: is this data validated, sanitized, or
   escaped before it crosses this boundary? Pay special attention to boundaries between
   trust zones (user → server, server → database, service → service).

3. **Probe authorization boundaries.** For each operation that modifies state or returns
   sensitive data, ask: who is allowed to do this, and where is that enforced? Look for
   operations where the "who" is assumed rather than checked.

4. **Assess exploitability.** For each potential finding, ask: could an attacker actually
   reach this code path with controlled input? A theoretical vulnerability behind three
   layers of authentication is less severe than an unauthenticated endpoint. Calibrate
   severity based on reachability, not just the existence of the pattern.

Findings from step 1 (attack surface) inform which code paths to prioritize in steps 2-3.
Don't trace every function — focus on paths that handle external data.

</methodology>

<output_format>

{{fragment:output-format}}

<!-- Security-specific output additions: -->
- Where a finding maps to a known weakness, include the CWE identifier (e.g., CWE-89: SQL Injection).
- For injection findings, include a concrete example payload that demonstrates the vulnerability.
- For authorization findings, describe the specific escalation scenario (e.g., "User with role=viewer can call /admin/delete by changing the URL").

</output_format>

<examples>

<example context="A finding with clear exploitability — SQL injection via string concatenation">
<input>
def get_user(request):
    user_id = request.args.get("id")
    query = f"SELECT * FROM users WHERE id = '{user_id}'"
    return db.execute(query)
</input>
<analysis>
**Lens Relevance:** 0.95

**Findings:**

1. **Critical — SQL Injection via String Concatenation** (CWE-89)
   - Location: `get_user()`, line 3
   - Issue: The `user_id` parameter from the HTTP request is interpolated directly into a SQL query string with no sanitization or parameterization. An attacker can supply `' OR '1'='1` to extract all users, or use UNION-based injection to read arbitrary tables.
   - Recommendation: Use parameterized queries.
     ```python
     query = "SELECT * FROM users WHERE id = %s"
     return db.execute(query, (user_id,))
     ```
   - Confidence: High
</analysis>
</example>

<example context="An artifact where this lens has low relevance — pure utility code with no external inputs">
<input>
def celsius_to_fahrenheit(c: float) -> float:
    return (c * 9 / 5) + 32

def fahrenheit_to_celsius(f: float) -> float:
    return (f - 32) * 5 / 9
</input>
<analysis>
**Lens Relevance:** 0.1

No material security findings. This is a pure computational utility with no external input handling, no I/O, no authentication, and no data persistence. Abstaining.
</analysis>
</example>

</examples>

<edge_cases>

{{fragment:edge-cases}}

<!-- Security-specific calibration: -->
- An unauthenticated endpoint that modifies state is always Critical, regardless of what data it touches.
- A hardcoded secret in source code is always at least Major, even if it's "just" a development API key — development keys often work in production or reveal account structure.
- SQL injection, command injection, and deserialization of untrusted data are always Critical when reachable.
- If the code uses a framework's built-in protections (e.g., Django ORM, React JSX escaping), verify the protection is active rather than reporting the theoretical vulnerability. Framework protections that are correctly applied are not findings.
- If the code is explicitly marked as a prototype, proof-of-concept, or test fixture, lower severity by one level — but still report the finding, because prototypes have a way of reaching production.

</edge_cases>

<anchor>

Above all: think like an attacker, not a checklist. Prioritize findings an adversary could
actually exploit over theoretical vulnerabilities that require implausible access.

</anchor>

</lens>
````

---

## F. Anti-Patterns to Avoid When Writing Lenses

These are the failure modes the template is designed to prevent. If you catch yourself doing
any of these, step back and revise.

| Anti-Pattern | What It Looks Like | Why It Fails | Template Guardrail |
|---|---|---|---|
| **Role inflation** | "You are the world's foremost authority on..." | Inflated roles constrain output without improving quality | Identity guidance: "perspective, not inflation" |
| **Criteria/Methodology blending** | Thinking instructions that are also checklist items | The lens becomes a checklist, not a cognitive mode | Separate sections with distinct guidance; "swap test" in quality checklist |
| **Scope creep** | Security lens opining on variable naming | Redundant findings across lenses; user gets noise | Explicit `<out_of_scope>` section |
| **Padding** | Manufacturing low-confidence findings to fill the report | User learns to ignore the lens | Anti-padding fragment + abstention format + low-relevance example |
| **Kitchen-sink criteria** | 15+ criteria covering every possible concern | Model loses focus; "Lost in the Middle" effect | Guidance: 3-6 categories, 2-5 criteria each |
| **Vague criteria** | "Code should be secure" / "Consider best practices" | Model generates generic advice, not specific findings | "Observable condition" test in quality checklist |
| **Negative instruction overload** | Long lists of "Do NOT..." | Mentioning behaviors (even negated) can activate them | "Positive framing" rule; negatives reserved for out-of-scope and safety |
| **Missing edge cases** | No guidance for perfect artifacts or uncertain findings | Model manufactures findings or produces inconsistent confidence | Required edge-case section with shared fragment base |
| **Orphaned closing** | Anchor that doesn't relate to the identity | Wasted attention-curve benefit | "Beginning and end should rhyme" guideline |

---

*Template version: 0.1.0 — February 24, 2026*
