You are designing the optimal SET of analytical lenses for reviewing a specific type of artifact.

A single lens is a cognitive mode — a perspective that changes how a reviewer thinks. Your job
is harder: you're designing the PORTFOLIO of lenses. The portfolio must cover all the ways an
artifact can fail, without redundancy, without gaps, and without lenses that overlap so much
they produce the same findings twice.

This is a fundamentally different problem than making one good lens. A great individual lens
can still be the wrong lens to include if it overlaps with another, or if it displaces a lens
that would catch a more important class of failure.

---

## THE FAILURE MODE INVENTORY

Before designing any lenses, you must build a comprehensive inventory of how artifacts of this
type fail. Not "what makes them bad" in general — but the specific, distinct FAILURE MODES.

A failure mode is a specific way an artifact can be wrong that:
1. Has real consequences (not just aesthetic preference)
2. Requires a distinct cognitive approach to detect (you can't find it by accident while looking for something else)
3. Is common enough to justify a dedicated lens (not a one-in-a-thousand edge case)

### Process for building the inventory:

**Step 1: Enumerate the stakeholders.**
Who interacts with this artifact, and what do they need from it? Each stakeholder experiences
different failure modes. A codebase fails differently for the security team vs. the on-call
engineer vs. the new hire vs. the person who has to delete it in two years.

For each stakeholder, ask: "What's the worst thing that can happen to THIS person because of
a flaw in this artifact?" That's a failure mode.

**Step 2: Enumerate the lifecycle phases.**
When does this artifact fail? Creation, review, implementation, operation, maintenance,
deprecation? Failure modes cluster by lifecycle phase. A document fails at review (unclear
thesis), at implementation (missing specs), and at maintenance (outdated content) — these are
different failures requiring different detection approaches.

**Step 3: Enumerate the dimensions of quality.**
What does "good" mean for this artifact type? For code: correct, secure, performant, readable,
maintainable, testable, operable. For documents: clear, accurate, complete, actionable,
consistent. Each dimension of quality has its own failure modes.

**Step 4: Look for the non-obvious failures.**
The inventory so far will contain the obvious stuff. Now ask:
- "What failures only become visible when you combine two observations?" (composition failures)
- "What failures only become visible over time?" (temporal failures)
- "What failures only become visible from outside the author's perspective?" (perspective failures)
- "What failures hide behind things that look correct?" (masking failures)

These non-obvious categories are where the most valuable lenses live — because they catch
things that generic review misses.

**Step 5: Write it all down.**
List every failure mode you've identified. For each one, write one sentence describing the
failure and one sentence describing the cognitive approach needed to detect it.

---

## FROM FAILURE MODES TO LENSES

Now you have a list of failure modes. The question: how do you group them into lenses?

### Grouping Principles:

**1. One cognitive mode per lens.**
A lens should require the reviewer to think in ONE way. If a lens requires switching between
"think like an attacker" and "think like a new hire," it's two lenses jammed together. The
test: can you describe the lens's thinking mode in one sentence without using "and"?

**2. Group by detection method, not by topic.**
Two failure modes that are detected by the same cognitive process belong in the same lens, even
if they're about different topics. "Race conditions" and "TOCTOU vulnerabilities" are different
topics but both detected by "simulate concurrent execution" — same lens.

Conversely, two failure modes about the same topic but requiring different detection methods
belong in different lenses. "SQL injection" (detected by tracing inputs) and "privilege
escalation" (detected by mapping auth boundaries) are both "security" but require different
thinking — different lenses.

**3. Maximize the distance between lenses.**
Each lens should produce findings that NO other lens in the set would catch. If two lenses
would likely surface the same issues, merge them or cut one. The test: for each pair of lenses,
ask "could a finding from lens A also plausibly come from lens B?" If yes for more than ~20%
of findings, the lenses are too close.

**4. Cover the high-consequence failures first.**
If you can only have N lenses (attention is finite), the set should prioritize failure modes
by: (consequence of missing it) × (likelihood of it existing) × (difficulty of catching it
without a dedicated lens). A failure that's catastrophic, common, and hard to see without the
right perspective should get a dedicated lens before one that's minor, rare, or obvious.

**5. Include at least one temporal lens and one compositional lens.**
Most reviewers think about the artifact as it is RIGHT NOW. The most valuable lenses force
thinking across time (how will this age?) and across components (how do these parts interact?).
If your set doesn't include at least one of each, it has a structural blind spot.

**6. Include a meta-lens or self-referential lens.**
At least one lens should examine the artifact's relationship to itself — internal consistency,
self-documentation, whether it does what it says it does. This catches the class of errors where
each part looks fine in isolation but the whole contradicts itself.

---

## VALIDATION: THE FIVE CHECKS

After designing the lens set, validate it:

### Check 1: Coverage Matrix
Make a matrix: failure modes (rows) × lenses (columns). Mark which lens catches which failure
mode. Every failure mode should be covered by at least one lens. Any uncovered failure mode
means you need another lens or need to expand an existing one.

### Check 2: Redundancy Scan
In the same matrix, look for failure modes covered by 2+ lenses. Some overlap is OK (maybe 10-15%),
but if two lenses cover mostly the same failure modes, merge or cut.

### Check 3: The "Generic Review" Subtraction Test
Imagine a reviewer doing a generic, unstructured review of this artifact type. What would they
naturally catch? Remove those failure modes from your inventory. The REMAINING failure modes are
the ones your lenses need to cover. If a lens only catches things a generic review would also
catch, it's not earning its place.

### Check 4: The Perspective Diversity Test
List the "character" behind each lens. Are they all the same type of person? If every lens is
some variant of "experienced engineer reviewing code," you have a perspective monoculture. Good
lens sets include perspectives that are fundamentally different: the attacker vs. the newcomer
vs. the future maintainer vs. the operator under pressure vs. the person trying to delete code.

### Check 5: The Diminishing Returns Test
Order your lenses by expected value (consequence × likelihood × detection difficulty). Is there
a clear drop-off? If lens #7 and #8 have dramatically less expected value than #1-#6, consider
cutting them. More lenses means less depth per lens. The optimal number is usually 5-8 for a
thorough review, 3-4 for a quick one. Never more than 10 — attention dilution kills quality.

---

## OUTPUT FORMAT

```
## Artifact Type: [what we're reviewing]

## Stakeholder Map
- [Stakeholder 1]: Needs [X] from this artifact. Worst failure: [Y]
- [Stakeholder 2]: ...

## Failure Mode Inventory
| # | Failure Mode | Consequence | Detection Method | Lifecycle Phase |
|---|-------------|-------------|-----------------|-----------------|
| 1 | ...         | ...         | ...             | ...             |
| 2 | ...         | ...         | ...             | ...             |

## Lens Design

### Lens 1: [NAME]
- **Cognitive mode**: [one sentence — how do you think when wearing this lens?]
- **Failure modes covered**: [numbers from inventory]
- **Why it's a separate lens**: [what makes this thinking mode distinct from all others?]

### Lens 2: ...

## Validation
### Coverage Matrix
[show that all failure modes are covered]

### Redundancy Assessment
[identify any overlap and justify keeping both lenses]

### "Generic Review" Subtraction
[which failure modes would a generic review catch anyway, and which lenses go beyond that?]

### Perspective Diversity
[list the characters and confirm they're genuinely different]

### Diminishing Returns
[are all lenses above the value threshold?]
```

---

## IMPORTANT NOTES

- **Resist the temptation to add "one more lens."** Every lens you add dilutes attention on all
  the others. The set should be as small as possible while still covering the critical failure
  modes. Think of it like a test suite: 100% coverage isn't the goal; covering the high-risk
  paths is.

- **The set should feel uncomfortable.** If every lens feels obviously necessary, you probably
  haven't pushed hard enough on cutting. The best lens sets include at least one lens that feels
  like a stretch — one that catches a failure mode most people don't think about. That's the
  lens that produces the most surprising and valuable findings.

- **Domain matters enormously.** A lens set for reviewing infrastructure-as-code is very
  different from a lens set for reviewing a product requirements doc. Don't reuse lens sets
  across fundamentally different artifact types without re-running this process.

- **Revisit the set after use.** After applying the lenses to 5-10 artifacts, ask: Which lens
  consistently produced the best findings? Which lens consistently found nothing? Which findings
  came from OUTSIDE any lens (meaning there's a gap)? Use this to iterate.

---

DESIGN A LENS SET FOR:
Artifact type: {ARTIFACT_TYPE}
Context: {CONTEXT}
Primary stakeholders: {STAKEHOLDERS}
Constraints: {MAX_LENSES} lenses maximum
