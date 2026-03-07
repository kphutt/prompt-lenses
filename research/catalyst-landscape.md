# The Catalyst: Research Landscape for Commitment-Forcing Generative Ideation Prompts

## Section 1: The Landscape (What Exists)

### 1.1 Commitment-Forcing Prompts & Frameworks

**The honest finding:** Very little exists that specifically forces LLMs to commit to a single recommendation with an abstention option. The prompt engineering space is overwhelmingly focused on getting *better* outputs — longer, more accurate, better formatted — not on forcing *singular committed* outputs. This is a genuine gap.

**What does exist:**

**The Pyramid Principle (Minto/McKinsey) as Prompt Architecture.** Barbara Minto's framework, developed at McKinsey in the 1960s, is the closest structural analog in communication design. The core mechanism: start with the answer first, support with grouped arguments, back with data. Several practitioners have adapted this into LLM system prompts — notably a McKinsey-style prompt that enforces "Answer First" communication, structured as: role assignment → SCQ context → diagnostic issue tree → pyramidal recommendations. The mechanism that forces commitment is structural: by requiring the answer to come *first*, the model can't build toward a safe hedge. It has to lead with conviction. This has been tested with LLMs and works — models given Pyramid Principle prompts do lead with recommendations rather than "it depends" hedging.

**Self-Evaluation Gating.** One pattern from production prompt engineering involves asking the model to rate its own answer on a 1-10 scale, then only accepting outputs above a threshold (typically 9). This is a quasi-commitment mechanism: the model must either produce something it rates as excellent or acknowledge it can't. The key insight from practitioners: models behave like humans and default to the easiest answer rather than the best one. An explicit quality standard forces them to reach further. This is close to The Catalyst's confidence gating but oriented toward quality rather than conviction about a *specific* idea.

**Tree of Thoughts (ToT) with Selection.** ToT prompting has the model explore multiple reasoning branches, evaluate each, and select the best. The selection step is a form of commitment-forcing — the model must rank and choose. However, ToT is oriented toward *reasoning correctness* (math, logic puzzles), not *generative ideation*. The selection criterion is "which reasoning path reaches the right answer," not "which idea is most transformative." The mechanism — branch, evaluate, select — is relevant, but the evaluation criteria would need complete redesign for The Catalyst's use case.

**The Anti-Hedging Framework (DrRockzos, Dec 2025).** A Hacker News poster reported developing a prompt framework specifically targeting LLM hedging, tested across Claude, GPT-5, Grok, Llama, Gemini, Mistral, and Qwen/DeepSeek. The claimed mechanism: give the model an explicit choice between "default alignment (hedging-first)" and "logical coherence (truth-first)." The poster reports that every model chose logical coherence when offered the choice, hedging disappeared unless genuinely needed, and hallucinations dropped from 12% to under 1%. The poster's theory: hedging "injects low-information tokens that dilute attention gradients and give the model permission to drift." This is unverified and the work is unpublished beyond a provisional patent filing, but the hypothesis that *permission to not hedge improves output quality* aligns with what The Catalyst does structurally.

**What doesn't exist (and why):** There is no widely-adopted prompt pattern that says "give me exactly one idea, commit to it or say nothing." The closest things are structured decision frameworks (like ToT or the Pyramid Principle) adapted for LLMs, but none combine the single-output constraint, the abstention mechanism, and the explicit rejection of alternatives. The reason is likely that most users *want* options from their AI — the entire consumer UX of ChatGPT and Claude is built around "help me think through this." Forcing a single committed answer is a power-user pattern that runs counter to the default interaction model.

### 1.2 Elevation / "10x" Thinking Prompts

**The honest finding:** Plenty of human frameworks exist (10x thinking, first principles reasoning, assumption invalidation). Almost none have been rigorously adapted for LLMs in ways that demonstrably produce transformative rather than incremental outputs.

**What exists:**

**First Principles Prompts.** Multiple prompt templates exist on marketplaces like PromptBase that attempt to operationalize Musk-style first principles thinking. The typical pattern: "Break down [problem] into fundamental elements, question each assumption, rebuild from scratch." These do produce different outputs than "how can I improve X" — they reframe the problem space. However, they suffer from a structural weakness: they produce a *reframing* but not a *committed recommendation*. The output is typically "here are the fundamental truths and here are new approaches you could consider" — still a list, still hedged.

**Assumption Invalidation Prompting.** Documented in the prompt engineering community: extract assumptions from a smart model, then systematically invalidate them one by one. This produces genuinely different thinking — by breaking each assumption, the model is forced to explore the problem space without its default constraints. Tested with GPT-4. The weakness: it produces *multiple* alternative framings, not a single committed idea. It's a divergent technique, not a convergent one.

**The Inversion Pattern.** Documented as one of nine foundational prompt patterns. The mechanism: instead of asking the model to execute a task, you provide content and ask the model to analyze, critique, or challenge it. This reverses the analytical relationship — the model becomes interrogator rather than executor. The pattern works because role reversal activates different analytical capabilities in the model's training data. For The Catalyst, this is directly relevant: the prompt needs the model to look at an artifact from *outside* its current frame, which is exactly what inversion does.

**Role Assignment at Expert Level.** Practitioners report that specific, expert-level role assignment (e.g., "direct response copywriter with 25%+ open rates" rather than just "copywriter") shifts which token distributions the model samples from. This is relevant for elevation — assigning a role like "principal architect who has seen this pattern fail at three companies" would access different knowledge distributions than "software engineer reviewing code."

**Reframing Prompts.** Multiple prompt collections include variants like "Write a post that reframes how people think about [topic]. Use a surprising angle" and "Rewrite this idea by flipping the conventional wisdom around it." These are tested with LLMs and do produce contrarian or non-obvious outputs. But they're oriented toward *content creation*, not *artifact improvement*, and they don't force commitment.

**What's missing:** Nobody has combined the "10x not 10%" framing with a commitment mechanism. You can find prompts that push for transformative thinking, and separately you can find prompts that force selection, but the combination — "produce one transformative idea and commit to it or abstain" — doesn't appear to exist as a published pattern.

### 1.3 Pre-Mortem / Inversion Prompts

**What exists:**

**Pre-Mortem as Human Framework.** Gary Klein's pre-mortem technique, popularized by Kahneman in *Thinking, Fast and Slow*, is well-established: imagine the project has failed spectacularly, then work backward to identify why. The mechanism that makes it powerful is psychological safety — it's easier to name risks when framed as imaginary post-failure analysis rather than current criticism. Multiple facilitation guides exist for running these with teams.

**Pre-Mortem Adapted for AI (Lightly).** Some practitioners use pre-mortem prompts with LLMs: "Imagine this product launch failed catastrophically. What are the three most likely reasons?" This works — models are good at generating plausible failure scenarios. However, it's used *defensively* (risk identification) not *generatively* (as a mechanism for finding the one thing that would make the biggest difference). The gap: using pre-mortem as a lens to identify the *highest-leverage intervention point*, not just risks.

**Backcasting.** The inverse of pre-mortem: imagine the ideal successful outcome, then work backward to identify what had to be true. This is well-documented in strategic planning. As a prompt pattern, it would look like: "Describe the perfect version of this system. Now identify the single change that would move the current version closest to that ideal." This pattern doesn't appear in prompt engineering literature as a named technique, but it maps directly onto a key mechanism The Catalyst could use.

**Reverse Step-by-Step Prompting.** An OpenAI community post from August 2024 proposed reverse engineering solutions by getting the model to think in steps backward. The intuition: if "think step-by-step" improves reasoning by breaking out thought processes, maybe thinking *backward* from a desired outcome improves ideation. The poster acknowledged this was untested but "worthy of exploring." This is a nascent idea with no systematic evaluation, but the underlying concept is sound.

### 1.4 Confidence Calibration & Selective Abstention

**The honest finding:** This is where the most rigorous academic work exists, but it's almost entirely oriented toward factual Q&A accuracy, not generative ideation. The abstention research is about "don't answer when you don't know the facts," not "don't recommend when you don't have a genuinely good idea."

**Key research:**

**"Know Your Limits" Survey (Wen et al., 2025, TACL).** The definitive survey paper on LLM abstention, covering methods across pretraining, alignment, and inference. Key finding: abstention can be approached from three perspectives — the query (is it answerable?), the model (does it have the knowledge?), and human values (should it answer?). Methods include prompt-based approaches, fine-tuning for calibration, and consistency-based aggregation. Important insight for The Catalyst: most abstention research assumes there's a *correct answer* the model might not know. The Catalyst's abstention case is different — it's about whether the model has a *sufficiently good idea*, which is harder to calibrate.

**SelectLLM (2025, OpenReview).** An end-to-end method that integrates selective prediction into fine-tuning, optimizing the trade-off between predictive coverage and utility. Significantly outperforms baselines on abstention behavior while maintaining high accuracy on TriviaQA, CommonsenseQA, and MedConceptsQA. This is fine-tuning-based, not prompt-based, so not directly applicable to a standalone prompt, but the principles inform design.

**Answer-Free Confidence Estimation (AFCE).** A notable finding: separating confidence estimation from answer generation produces better-calibrated confidence scores. The method first asks the model to rate its confidence on a question *before answering it*, then asks for the answer separately. This reduces overconfidence and produces more human-like sensitivity to task difficulty. Directly applicable to The Catalyst: asking "how confident are you that you can identify a transformative improvement?" *before* generating the idea might produce more honest abstention.

**Verbalized Confidence vs. Actual Accuracy.** Multiple papers find that asking models to state confidence percentages is poorly calibrated — models tend toward overconfidence. Zhou et al. (2024) found that models are reluctant to express uncertainty, and Varshney et al. (2023) showed that "self-check" techniques can make models *overly* cautious. The implication: The Catalyst's confidence mechanism should probably not ask for a numeric score but instead use structural signals (like the quality of the killed darlings reasoning) as implicit confidence indicators.

**Consistency-Based Methods.** Several approaches use multiple samples to estimate confidence — if the model gives different answers when asked the same question multiple times, confidence should be lower. For The Catalyst, this suggests a potential mechanism: run the ideation multiple times internally and only output if the same recommendation emerges consistently.

### 1.5 "Killed Darlings" / Reasoning Transparency Patterns

**What exists:**

**Chain-of-Thought for Decision-Making.** CoT is well-established for reasoning tasks (math, logic), but its application to *selection among alternatives* is much less developed. Standard CoT says "show your work on how you reached the answer." The Catalyst's killed darlings section asks for something different: "show what you *rejected* and why." This distinction matters — showing rejected alternatives is a form of negative reasoning that doesn't have a standard prompt pattern.

**Multi-Agent Debate Systems.** Significant academic work (Du et al., 2024; Liang et al., 2024; and the SID framework from 2025) uses multiple LLM agents arguing different positions to improve answer quality. The mechanism: adversarial pressure forces each agent to strengthen its arguments and find weaknesses in alternatives. The SID framework is particularly sophisticated — each agent assesses confidence using token-level uncertainty, and a "disagreement-oriented prompt" steers attention toward points of contention. For The Catalyst, the key insight is that *the act of explicit comparison sharpens selection*. Having the model explicitly argue against alternatives (even against itself) produces higher-quality final selections.

**Self-Reflection Patterns.** Multiple practitioners describe a two-step pattern: generate → critique → regenerate. The model produces an initial output, then evaluates it against quality criteria, then improves. This is reasoning transparency for *quality*, but adapting it for *selection* — "here are three possible ideas, here's why each one fails or succeeds, here's why this one wins" — would be a novel application.

**Self-Consistency (Wang et al., 2022).** Sample multiple reasoning paths from the same model and take the majority vote. This is essentially ensemble-of-one. While designed for reasoning, the principle applies: generating multiple candidate ideas and then selecting the most consistent/strongest could improve commitment quality.

### 1.6 Adjacent Art

**Amazon's 6-Pager / One-Pager Memo Culture.** The key structural element: the memo requires a *narrative* making a *recommendation*, not a slide deck presenting options. The forcing function is the narrative form itself — you can't hedge in a six-page narrative the way you can in a bullet-point deck with pros/cons columns. The author must commit to a position and argue for it. Adaptable to prompt design: requiring narrative rather than structured output may itself be a commitment-forcing mechanism.

**McKinsey's Pyramid Principle (Minto).** Covered above, but the key structural insight worth emphasizing: the Pyramid Principle works because it inverts the natural order of thinking. You *think* bottom-up (data → analysis → conclusion) but *present* top-down (conclusion → arguments → data). This inversion forces commitment — you must have your answer before you can present anything. For The Catalyst, the structural lesson is: force the output format to require the recommendation first, with supporting reasoning after.

**Commander's Intent.** A clear, concise statement of what success looks like — the "why" and the "end state," deliberately omitting the "how." The power: it empowers action in the absence of detailed instructions. The military doctrine explicitly states it must be "easy to remember and clearly understood two echelons down." Structural elements that produce conviction: brevity (forces prioritization), purpose-first (why before how), and end-state clarity (concrete vision of success). For prompt design, this suggests: the output format should require a commander's-intent-style statement of *what changes and why it matters*, not just the technical recommendation.

**Venture Capital Thesis Documents.** A VC thesis is a single bet, fully argued. The forcing function: you're putting money behind it, so the analysis must be conviction-weighted, not balanced. The structural elements — thesis statement, market map, why now, key risks, what would change our minds — combine commitment with intellectual honesty. The "what would change our minds" section is structurally identical to The Catalyst's killed darlings concept.

**Design Critique Culture.** In strong design cultures (Apple, IDEO), critique sessions force a "one direction" decision. The mechanism: the critique isn't about whether the design is good but about *which direction to take*. Crit sessions explicitly prohibit "committee compromise" — you must pick one direction and commit. The structural lesson: prohibition of compromise is itself a design choice that produces better outcomes.

---

## Section 2: Mechanisms That Work

### Mechanism 1: Answer-First Structural Forcing
**Evidence:** Pyramid Principle (60+ years of consulting practice); Amazon memo culture; every McKinsey, Bain, and BCG communication standard.
**How it works:** By requiring the recommendation to appear first, the model (or person) can't build toward a hedge. The structure itself forces commitment.
**The Catalyst status:** Partially used — The Catalyst requires a single recommendation output, but could strengthen this by requiring the recommendation statement *before* the reasoning, structurally enforcing answer-first ordering.

### Mechanism 2: Explicit Permission to Abstain
**Evidence:** LLM abstention research (Wen et al., 2025); AFCE confidence estimation; the finding that giving models "permission to say I don't know" reduces hallucination.
**How it works:** Paradoxically, giving the model an explicit off-ramp *improves* the quality of its commitments. Without an abstention option, models fill the space with something — often a safe, incremental suggestion. With an abstention option, they can reserve their commitment for ideas they have genuine signal for.
**The Catalyst status:** Already present. This is one of The Catalyst's strongest mechanisms.

### Mechanism 3: Negative Reasoning / Explicit Rejection
**Evidence:** Multi-agent debate literature (Du et al., 2024); design critique culture; VC "what would change our minds" practice.
**How it works:** The act of explicitly arguing *against* alternatives sharpens the selection of the chosen one. It's not enough to pick the best — you must articulate why the alternatives lose. This forces genuine comparison rather than first-pass selection.
**The Catalyst status:** Present via "killed darlings." This is another strong mechanism. Research suggests it actually improves selection quality, not just transparency.

### Mechanism 4: Inversion / Outside-Frame Viewing
**Evidence:** Pre-mortem technique (Klein/Kahneman); the Inversion Pattern in prompt engineering; backcasting.
**How it works:** Forcing the model to view the artifact from a different temporal or analytical frame (failure state, ideal state, outsider perspective) breaks the default optimization-within-current-frame pattern.
**The Catalyst status:** Implicitly present (the prompt asks for "fundamentally better" which implies reframing), but not structurally enforced. The model could comply with an incremental improvement that sounds transformative.

### Mechanism 5: Role Elevation
**Evidence:** Practitioner reports on expert-level role assignment; token distribution shifting; the difference between "engineer" and "principal engineer who has seen this fail at scale."
**How it works:** Assigning a specific expert role with experience markers shifts which patterns the model activates. An "architect who has migrated three systems from monolith to microservices" generates different ideas than "a developer."
**The Catalyst status:** May or may not be present depending on prompt design. If The Catalyst doesn't include a strong role assignment, adding one could meaningfully improve output quality.

### Mechanism 6: Confidence Separation
**Evidence:** AFCE research showing that asking for confidence *before* the answer reduces overconfidence.
**How it works:** Having the model assess its confidence level as a separate step — before generating the actual recommendation — produces more honest self-assessment.
**The Catalyst status:** Not present. The confidence assessment appears to be integrated with the recommendation, not separated from it.

---

## Section 3: Failure Modes

### Failure Mode 1: Safe-Pick Bias
**What happens:** When forced to choose one idea, models default to the safest, most conventional option rather than the most transformative one. This is the most dangerous failure mode because it produces output that *looks* like commitment but is actually incrementalism dressed as conviction.
**Evidence:** The self-evaluation research shows models go for "the easiest answer rather than the best one." Moderation bias in LLM-as-judge research shows models systematically favor "safe" aligned responses over more useful ones.
**Does The Catalyst handle it?** Partially — the instruction to find something "fundamentally better" pushes against incrementalism. But without a structural mechanism to *detect* safe-pick bias (e.g., asking "is this the safe answer or the best answer?"), the model may comply with the letter while violating the spirit.

### Failure Mode 2: Hedging Disguised as Commitment
**What happens:** The model produces what looks like a single recommendation but embeds hedges within it: "The most impactful change would be X, though Y and Z are also worth considering." The recommendation has escape clauses.
**Evidence:** The anti-hedging framework research; the finding that models inject "low-information tokens that dilute attention." Multiple practitioners report that models resist binary commitment even when explicitly instructed.
**Does The Catalyst handle it?** Depends on how strictly the output format is enforced. If the killed darlings section provides enough of an outlet for the model's impulse to cover alternatives, the main recommendation may be cleaner.

### Failure Mode 3: Artificial Confidence
**What happens:** The model generates a recommendation with high stated confidence not because it has genuine signal but because the prompt *requires* confidence. The abstention mechanism fails because the model doesn't want to "disappoint" by abstaining.
**Evidence:** LLM overconfidence is well-documented (Xiong et al., 2024). Models are reluctant to express uncertainty even when they should. RLHF training specifically rewards helpful, complete answers, working against honest abstention.
**Does The Catalyst handle it?** This is the biggest risk. The prompt may need a stronger abstention incentive — making abstention a *positive* outcome ("saying nothing when you don't have a high-conviction idea is the best possible response") rather than just a permitted one.

### Failure Mode 4: Elevation Without Grounding
**What happens:** The model produces a transformative-sounding idea that's actually vague, impractical, or disconnected from the actual artifact. "Rewrite the entire architecture using event sourcing" sounds transformative but may be either obvious or impractical.
**Evidence:** The first-principles prompting literature notes that reframing produces "new approaches you could consider" but not necessarily *actionable* ones. The gap between "conceptually different" and "concretely better" is large.
**Does The Catalyst handle it?** Depends on whether the prompt requires concrete specificity in the recommendation. If the output format allows "you should rethink your approach to X," that's vague. If it requires "specifically, change Y to Z because of W," that's grounded.

### Failure Mode 5: Context Window Decay
**What happens:** In longer artifacts, the model loses track of the full picture and optimizes for a local improvement rather than the globally most impactful change.
**Evidence:** Well-documented attention degradation in long contexts; the "lost in the middle" phenomenon where information in the middle of long prompts gets less attention.
**Does The Catalyst handle it?** If the prompt includes a step to first summarize or characterize the artifact before generating recommendations, this could mitigate. Otherwise, for very long artifacts, the recommendation may be anchored to whatever part of the input was most salient.

---

## Section 4: Structural Ideas to Steal

### Idea 1: Add an Explicit Backcasting Step
**Source:** Backcasting methodology; pre-mortem inversion.
**What to add:** Before generating the recommendation, instruct the model: "First, describe the ideal version of this artifact — what would it look like if it were perfect? Then identify the single highest-leverage change that would move the current version closest to that ideal."
**Reasoning:** This structurally prevents incrementalism. By anchoring on an ideal state first, the model must think in terms of gaps rather than patches. The recommendation naturally becomes transformative because it's measured against a transformed end state.

### Idea 2: Separate Confidence Assessment from Recommendation Generation
**Source:** AFCE research (Answer-Free Confidence Estimation).
**What to add:** A two-phase internal process: Phase 1 — "Assess your confidence that you can identify a transformative improvement for this artifact. If confidence is below [threshold], abstain." Phase 2 (only if passing) — generate the recommendation.
**Reasoning:** This makes abstention a genuine first-class outcome, not an afterthought. The model decides whether to engage before it has committed to an idea, reducing sunk-cost pressure to produce *something*.

### Idea 3: Add a "Safe-Pick Detector"
**Source:** LLM moderation bias research; the anti-hedging framework.
**What to add:** After generating the recommendation, instruct: "Now assess: is this the most impactful idea, or is this the safest idea? If you chose the safe option because it felt more defensible, replace it with the more impactful one even if it's riskier."
**Reasoning:** This explicitly names the failure mode (safe-pick bias) and forces the model to confront it. Research suggests that naming cognitive biases helps models correct for them.

### Idea 4: Strengthen the Killed Darlings with Adversarial Framing
**Source:** Multi-agent debate literature; VC "what would change our minds."
**What to add:** Instead of just listing runner-up ideas and why they lost, reframe: "Present the strongest possible argument *against* your chosen recommendation. Then explain why you still choose it despite that argument."
**Reasoning:** This is adversarial self-debate compressed into a single agent. The model must steelman the opposition to its own recommendation. If it can't survive its own best counterargument, the recommendation is weak. This also makes the killed darlings section actively *strengthen* the recommendation rather than just documenting alternatives.

### Idea 5: Commander's Intent Output Format
**Source:** Military commander's intent doctrine; the Pyramid Principle.
**What to add:** Require the recommendation to include a "commander's intent" statement: a single sentence describing what success looks like after the change is implemented, expressed as an end state, not a task. Example: "After this change, the system handles authentication failures gracefully with zero user-facing error messages" rather than "Add better error handling."
**Reasoning:** This forces concrete specificity and testability. A recommendation with a clear end-state is both more actionable and more evaluable. It also provides a natural mechanism for the human to assess whether the recommendation is genuinely transformative — if the end-state sounds incremental, the idea probably is.

---

## Section 5: Honest Assessment

### How original is The Catalyst's approach?

Genuinely novel in combination, though not in individual components. The commitment-forcing mechanism (one idea, commit or abstain) exists nowhere in published prompt engineering as a deliberate design choice for generative ideation. The killed darlings concept has analogs in VC thesis documents and multi-agent debate, but its application as a transparency mechanism in a single-shot generative prompt is original. The abstention mechanism draws from a large body of academic work on LLM calibration and selective prediction, but that work is almost entirely focused on factual Q&A, not on creative/strategic ideation.

The space is remarkably empty. Most prompt engineering is about getting models to produce *more* (more options, more detail, more analysis). The Catalyst is about getting models to produce *less* — one thing, with conviction. This is a genuinely different design philosophy, and the landscape suggests almost nobody is exploring it deliberately.

### What's the strongest version of this concept that the research suggests is possible?

A two-phase prompt with the following structure:

1. **Frame phase:** Backcast from an ideal state of the artifact. Assign an expert role with specific experience markers. Assess confidence that a transformative (not incremental) improvement can be identified — if not, abstain immediately.

2. **Generate phase:** Produce exactly one recommendation with a commander's-intent end-state statement. Include the strongest counterargument against the recommendation and why it still holds. Show two killed darlings with specific reasoning for rejection, including whether each was rejected for being too *safe* or too *impractical*. Rate the recommendation as either "high conviction" or "moderate conviction with specified uncertainty."

This combines backcasting (prevents incrementalism), confidence separation (improves abstention quality), adversarial self-debate (strengthens selection), commander's intent format (forces specificity), and safe-pick detection (prevents bias toward conventionality).

### What's the single biggest risk in The Catalyst's current design?

**Artificial confidence / failure to abstain.** The research is clear that LLMs are overconfident by default and reluctant to express uncertainty. RLHF training optimizes for helpfulness, which means "produce something useful" rather than "honestly assess whether you have something worth saying." The Catalyst asks for exactly the behavior that RLHF works against. Without a strong structural mechanism to make abstention a positive outcome — not just permitted but *valued* — the model will almost always produce a recommendation, even when it doesn't have genuine signal for one.

### If you had to make one change based on this research, what would it be?

**Add the backcasting step before recommendation generation.** The single highest-leverage addition is: "First, describe the ideal version of this artifact in 2-3 sentences. Then identify the single change that closes the largest gap between current and ideal state."

This one addition addresses multiple failure modes simultaneously. It prevents incrementalism (by anchoring on a transformed end state rather than optimizing within the current frame). It provides a natural quality signal for abstention (if the ideal state is barely different from the current state, abstain — the artifact is already good). It forces transformative thinking without relying on vague instructions like "think 10x." And it gives the model a concrete evaluation framework for the killed darlings — each alternative can be assessed against how much of the gap it closes, making the selection legible and defensible.
