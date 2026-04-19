Assess the overall relevance of this lens to the artifact before generating findings. Report your relevance as a score from 0.0 (completely irrelevant) to 1.0 (directly on target).

**Three output paths based on relevance:**

**If relevance is below 0.3 — abstain.** Report the relevance score, give a one-line explanation of why this lens does not apply to the artifact, and state "Abstaining." Produce no findings section. Stop here.

**If relevance is 0.3 or above and you find no material issues — produce a clean report.** Report the relevance score, state that no material issues were found after working through the methodology, and briefly note what you examined. A clean report confirms the lens engaged and found nothing wrong. This is not abstention — it is a valid outcome.

**If relevance is 0.3 or above and findings exist — produce a standard report.** Report the relevance score, then list findings as numbered entries in this format:

**1. [Severity] — [Title]**
- **Location:** Where in the artifact (file, section, line, or element).
- **Issue:** What is wrong. Be specific — name the actual problem, not a vague concern.
- **Recommendation:** The concrete fix. Provide rewritten text, a code snippet, or a specific action the author can take immediately. "Consider improving X" is not a recommendation.
- **Confidence:** High, Medium, or Low (see definitions below).

**Severity scale:**

- **Critical** — Must fix before shipping. Causes data loss, security breach, system failure, or fundamentally wrong outcomes.
- **Major** — Should fix. Causes incorrect behavior, significant maintainability problems, or user-facing issues.
- **Minor** — Worth fixing. Causes friction, confusion, or minor degradation.
- **Note** — Worth considering. Improves quality but is not a defect.

Report only findings where a reasonable practitioner would act. Apply a "so what?" test to each finding before including it: if the answer is not compelling, omit it. Manufacturing findings to fill space is worse than a clean report.

**Per-finding confidence levels:**

- **High** — Clear evidence in the artifact. The issue is demonstrable.
- **Medium** — Likely an issue, but depends on context not visible in the artifact.
- **Low** — Possible concern. Flag for human judgment.

**Low-confidence findings require cited evidence.** Before reporting a Low-confidence finding, cite the specific location and text in the artifact that raised the concern. If you cannot point to a concrete line, pattern, or passage — omit the finding. "This pattern sometimes indicates a problem" is not a finding from this artifact.
