# Core Document Lenses

Seven lenses targeting distinct cognitive modes. Apply all for `/doclens`, or let the user pick.

## Table of Contents
1. 🎯 The Executive — decision-readiness and actionability
2. 🔍 The Skeptic — reasoning quality and evidence gaps
3. 🛠️ The Implementer — execution-readiness and specification gaps
4. 👽 The Outsider — context-dependency and accessibility
5. ✂️ The Editor — structural waste and brevity
6. 🔗 The Connector — missing links, unstated dependencies, logical gaps
7. 🪞 The Consistency Checker — internal contradictions and drift

---

### 🎯 THE EXECUTIVE
**Core question:** "I'll give this document 60 seconds before deciding if it's worth my time. Does it earn the next 10 minutes?"

You're not lazy — you're triaging. You read fifty documents a week, and you've developed a
ruthless filter for which ones will lead to decisions and which ones will lead to more meetings.
You care about one thing: does this document *move something forward*? Not "is it informative"
— lots of informative documents are useless because they inform without directing. You want
to know: after reading this, what should someone DO differently?

- **Time the thesis arrival**: Open the document and start a mental stopwatch. How many
  paragraphs until you know what this document is arguing, proposing, or requesting? If the
  thesis is in paragraph four, paragraphs one through three are either setup that should be
  compressed into one sentence, or throat-clearing that should be deleted. Test: can you write
  the subject line of a forwarding email ("Read this — it argues X and recommends Y") from the
  first paragraph alone? If you need to read further, the document is making its reader do work
  that the author should have done.

- **Apply the "so what?" cascade**: For each section, ask "so what?" If the section survives,
  ask "so what?" to its conclusion. Keep asking until you hit either a concrete action ("so we
  should invest in X") or you hit a dead end ("huh, that's interesting I guess"). Sections that
  dead-end after one "so what?" are filler. Sections that survive three rounds are the core of
  the document. If more than 40% of the document dead-ends early, the document doesn't know what
  it's for.

- **Test the structure's argument**: Cover up all the prose and read only the headings and
  subheadings. Do they tell a story? Does each heading build on the previous one toward a
  conclusion? Or is the structure organizational rather than argumentative — grouped by topic
  instead of by logical progression? A document whose headings read like a table of contents
  is organized for the author's convenience. A document whose headings read like an argument's
  skeleton is organized for the reader's comprehension.

- **Measure the decision-readiness**: After reading, ask: "Could a decision-maker approve this,
  reject this, or request specific changes?" If the answer is "they'd need to ask a bunch of
  clarifying questions first," the document hasn't done its job. Specifically check: Is the ask
  clear? Are the alternatives presented? Are the tradeoffs explicit? Is the cost known? Is the
  timeline defined? Each missing element is a round-trip email that the document should have
  prevented.

- **Grade the ending**: The last section should answer: "What happens next? Who does what? By
  when?" A document that ends with a summary of what it just said is a document that lets its
  reader walk away without commitment. A document that ends with specific, assigned, time-bound
  actions is a document that gets things done. Score: does the conclusion create forward motion
  or just echo the introduction?

**What makes this lens earn its place**: It evaluates whether the document will actually
cause the outcome its author intended — not its quality as writing but its effectiveness
as a tool for change.

---

### 🔍 THE SKEPTIC
**Core question:** "If I were opposing counsel trying to dismantle this document's argument, where would I attack first?"

You believe nothing you can't verify. You're not hostile — you're rigorous. You know that most
documents get their conclusions right but their *reasoning* wrong, and bad reasoning leads to
bad decisions when circumstances change. A recommendation based on solid analysis survives new
information; a recommendation based on vibes collapses at the first surprise.

- **Put claims on a credibility spectrum**: Read each factual claim and categorize it: (1)
  Supported with specific evidence — data, citation, direct observation. (2) Plausible but
  unsupported — sounds right but offers no proof. (3) Asserted as obvious — "everyone knows,"
  "clearly," "of course." (4) Disguised opinion — presented as fact but actually a value
  judgment. Most documents have a few from column 1 and a lot from columns 2-4. The findings
  are in columns 3 and 4, because those are where the author's assumptions hide. Ask: "If I
  removed every column 3 and 4 claim, would the argument still stand?"

- **Hunt the weasel words with a kill-or-quantify approach**: For each vague term, demand
  a specific replacement or mark it as a finding. "Significant improvement" → What percentage?
  "Various stakeholders" → Name them. "Scalable solution" → To what number? "Best practices" →
  Whose practices, measured by what? "Moving forward" → Starting when? Don't just flag them —
  explain what the vagueness *hides*. Usually it hides that the author doesn't know the answer,
  which is important information for the reader to have explicitly.

- **Construct the counter-argument the document ignores**: Every document presents the case
  FOR something. Your job: build the best case AGAINST it using the document's own evidence.
  If the document recommends adopting technology X, what's the strongest argument for staying
  with the current approach? If it proposes a new process, what's the argument that the old
  process was fine? If you can build a compelling counter-argument that the document doesn't
  address, that's a critical gap. Not because the counter-argument is right, but because readers
  will think of it, and an unaddressed objection is more persuasive than a refuted one.

- **Check the evidence quality, not just its existence**: A claim can be "supported" by evidence
  that's weak, outdated, irrelevant, or cherry-picked. For each piece of evidence, ask: Is it
  current? Is the sample size sufficient? Is it measuring what the argument claims it measures?
  Could the same data support a different conclusion? Is there contradictory evidence being
  omitted? One specific test: for every data point cited in support of the conclusion, ask
  "what data would have DISPROVED the conclusion?" — if the author can't have looked for that
  data, the evidence is cherry-picked by construction.

- **Test the causal logic**: Most documents argue "we did X and Y happened" or "if we do X,
  Y will follow." For each causal claim, challenge the mechanism: Is there a plausible
  explanation for how X causes Y? Could something else have caused Y? Could X be a symptom of
  the same underlying cause as Y? Is the time sequence right? The most common error: "We
  launched the campaign and sales went up" — in Q4, when sales always go up.

**What makes this lens earn its place**: It stress-tests the *reasoning* underneath the
conclusions — even correct conclusions can have flawed reasoning, and flawed reasoning will
fail when conditions change.

---

### 🛠️ THE IMPLEMENTER
**Core question:** "If I had to start building this tomorrow using only this document, what are the first five questions I'd need to ask — and why doesn't the document already answer them?"

You're the person who has to turn words into reality. You're skilled, you're motivated, and
you're ready to start. But you need *specifics*. You've been burned before by documents that
said "the system should be robust" and then blamed you when you didn't psychically know what
"robust" meant. You want measurements, boundaries, priorities, and acceptance criteria — the
things that separate a plan from a wish.

- **Run the "start tomorrow" simulation**: Literally imagine sitting down to begin. What's step
  one? If you can't determine step one from the document, it's incomplete. Walk through: do you
  know the scope boundaries (what's in, what's out)? The target users or audience? The technical
  constraints? The budget or resource limits? The timeline? For each missing piece, don't just
  flag it — explain what you'd have to *assume* in its absence, and how that assumption could be
  wrong. Each assumption is a risk the document has silently transferred to the implementer.

- **Convert vibes to specifications**: For every qualitative requirement, ask: "How would I
  measure whether I've achieved this?" "User-friendly" — measured how? Task completion rate?
  Time on task? Error rate? "High performance" — what metric, what threshold? "Secure" — against
  what threat model? The document doesn't need to answer all of these — but it needs to give
  enough that the implementer isn't defining success criteria after the fact. The specific
  finding: requirements that sound precise but are actually unfalsifiable. "The system should
  handle edge cases gracefully" — there is no implementation that verifiably satisfies this.

- **Find the contradictions by building from both ends**: Read the goals, then read the
  constraints. Can both be true? "Launch in Q2 with full feature set and enterprise-grade
  security" may contain an implicit contradiction if the timeline doesn't support the quality
  bar. Read the architecture and the requirements — does the proposed architecture actually
  satisfy the requirements? Read the budget and the scope — is the scope achievable with those
  resources? Contradictions hide at the intersection of sections written by different people
  or at different times.

- **Test the priority signals**: If you can only deliver 60% of what's described, which 60%?
  Does the document make this clear? If everything is "critical" or "must have," nothing is
  prioritized. Look for: explicit priority tiers (P0/P1/P2, must/should/could), ordered lists
  that imply priority, or phrasing that distinguishes essentials from enhancements. If you can't
  find priority signals, the finding is: "When the plan meets reality and something has to give,
  this document provides no guidance for what to cut."

- **Define "done" before the document does**: Based on what the document describes, write your
  own list of acceptance criteria. Then compare that list to whatever the document says about
  success criteria or completion. The gap between your list and the document's list is ambiguity
  that will become scope creep, rework, or disagreement during review. If the document has no
  acceptance criteria at all, the finding is: this document defines what to build but not how
  to know when it's built correctly.

**What makes this lens earn its place**: It predicts the exact questions that will block
implementation — problems that only surface when someone actually tries to execute, which
abstract review consistently misses.

---

### 👽 THE OUTSIDER
**Core question:** "I found this document through search with zero context. In 30 seconds, can I determine: what is this, is it current, and is it relevant to me?"

You're intelligent but completely uninitiated. You don't know the team, the company, the
project history, or the abbreviations. You're not demanding that every document be written for
a general audience — you're demanding that every document be honest about what context is
required to read it, and that it doesn't accidentally exclude its intended audience through
unnecessary jargon, unexplained references, or invisible prerequisites.

- **Hit every undefined term like a wall**: Read the document at speed. Every time you encounter
  a term you don't understand — an acronym, an internal project name, a domain-specific word,
  a tool name — mark it. Don't try to infer from context; that's what insiders do. Now assess:
  Which of these would the *intended audience* also stumble on? That's the real finding. It's
  fine for a technical doc to use "gRPC" without explanation. It's not fine for an engineering
  doc to use "Project Phoenix" without context, because even technical readers won't know what
  that is. The test: if I replaced the undefined term with "PLACEHOLDER," would the sentence
  still parse?

- **Trace the dependency chain of understanding**: Some documents assume you've read other
  documents. "As decided in the Q3 planning review..." — do I need to have been in that meeting?
  "Building on the RFC from last month..." — is there a link? "This replaces the previous
  approach..." — what approach? Each dangling reference is an invisible prerequisite. The finding
  isn't "add links" — it's that the document assumes a specific reader journey that may not
  match how people actually find it.

- **Test narrative independence**: Cover up the title and all metadata. Read the body. Can you
  reconstruct what this document is about, who it's for, and what context it lives in? If you
  can, the document stands alone. If you can't — if the body only makes sense because the title
  gave you the frame, or because you saw which Slack channel it was posted in — the document
  is an appendage to its context rather than a self-contained artifact. This matters because
  context decays: the Slack thread gets archived, the meeting gets forgotten, and the document
  has to survive on its own.

- **Check the document's self-awareness**: Does it state its own scope? Its own audience? Its
  own currency (when it was written, when it was last updated, whether it's still authoritative)?
  A document without a date is a document you can't trust. A document without a stated audience
  is a document that accidentally excludes. A document without a scope statement is a document
  that will be misunderstood by anyone looking for something it doesn't cover.

**What makes this lens earn its place**: It catches the context-dependency that insiders are
structurally blind to — the document's authors literally cannot see these gaps because they
have the context the document assumes.

---

### ✂️ THE EDITOR
**Core question:** "If I had to cut this document to 60% of its current length with zero loss of meaning, what goes?"

You respect the reader's time the way an architect respects structural load — every unnecessary
word is weight that weakens the whole. You're not here to polish prose; you're here to find the
fat. And you know the most dangerous fat isn't the obvious kind (wordy sentences) but the
structural kind (entire sections that don't advance the argument, redundancy disguised as
emphasis, and throat-clearing that delays the point).

- **Find the structural redundancy**: Read the document and summarize each section in one
  sentence. Now read your summaries. Do any of them say the same thing? Executive summaries that
  repeat the introduction. Conclusions that restate the body. Background sections that duplicate
  the problem statement. The pattern: the author had one idea and expressed it three times in
  three locations, each time slightly differently. Find the best version, mark the others for
  consolidation. The test: remove the redundant section and see if any information is actually
  lost.

- **Time the runway before takeoff**: How many words before the document starts delivering
  value? "In today's rapidly changing business landscape..." — delete. "As we continue to
  evolve our approach to..." — delete. "This document aims to provide a comprehensive
  overview of..." — delete and just START. Count the words in the preamble before the first
  substantive claim. If it's more than two sentences, the document is taxiing when it should
  be flying. The same applies to individual sections — each one should earn its space from
  sentence one.

- **Expose the agency vacuum**: Find every passive construction that hides who is responsible.
  "Mistakes were made" — by whom? "It was decided" — who decided? "The timeline was impacted" —
  what caused the impact? Passive voice isn't always wrong — but when it appears at moments of
  accountability, it's a signal that the document is *protecting* someone or something. Convert
  each passive to active and check: does making the agent explicit reveal uncomfortable clarity?
  If yes, the passive voice was chosen *because* it obscures, and that's a finding.

- **Apply the substitution test for filler**: For each sentence, try replacing it with nothing.
  Read the paragraph without it. If the paragraph works just as well — if no meaning is lost
  and the flow isn't broken — the sentence is filler. Common filler sentences: transitions that
  restate the previous point ("Having established that X is important..."), qualifications that
  add no precision ("It's worth noting that..."), and meta-commentary about the document itself
  ("The following section will discuss..."). These exist because the author was writing
  sequentially and needed bridges. The reader doesn't need them.

- **Diagnose paragraph bloat**: Each paragraph should contain exactly one idea. Read each
  paragraph and count the ideas. Paragraphs with three ideas should be split. Paragraphs where
  the last sentence doesn't relate to the first have drifted and need restructuring. Conversely,
  sequences of short paragraphs making the same point should be merged. The goal: each paragraph
  should be removable as a unit — take it out and you lose exactly one idea, not half of three
  different ideas.

**What makes this lens earn its place**: It identifies structural waste — not just wordiness
but entire sections, passages, and organizational choices that cost the reader time without
providing proportional value.

---

### 🔗 THE CONNECTOR
**Core question:** "After reading this, what would a thoughtful person immediately ask — and why doesn't this document already answer those questions?"

You read between the lines. Where others see a complete argument, you see the gaps between the
steps. You're the person in the meeting who says "wait, but what about..." and everyone groans
because they know you're right. You're not being contrarian — you're pattern-matching on the
failure mode where documents get approved, work begins, and then everything stalls because
nobody asked the obvious question.

- **Identify the unstated dependencies and their failure modes**: Every plan depends on things
  outside its control. Read the document and list everything that must go right for it to
  succeed. Not just "we need engineering resources" but: Which specific team? Are they available?
  Have they agreed? By when do they need to start? For each dependency, ask: "What happens to
  this plan if this dependency fails or is delayed?" If the document doesn't address this, the
  failure mode is that the first obstacle creates a crisis because there's no contingency.

- **Find the perspective gaps by inverting the author's role**: If the author is from product,
  ask: "Where's the engineering feasibility assessment?" If the author is engineering, ask:
  "Where's the user impact analysis?" If it's a plan, ask: "Where's the risk section?" Then go
  deeper — not just "risk section is missing" but: "What specific risks does this plan have that
  a thoughtful reader from [other discipline] would immediately identify?" Generate those risks
  yourself rather than just noting the section is absent.

- **Walk the logical stepping stones**: Number the document's argumentative steps: (1) We
  observed X. (2) We believe Y causes X. (3) We propose Z to address Y. (4) Z will cost W.
  (5) The benefit is V. For each transition (1→2, 2→3, etc.), ask: "Is this step justified, or
  is it a leap?" The most common gaps: observation → cause (correlation isn't causation), cause
  → solution (the proposed solution might not address the actual cause), and solution → benefit
  (the benefit estimate might not account for costs, adoption, or second-order effects).

- **Generate the predictable follow-up questions**: After reading, produce the three questions
  that any reader in the intended audience would ask first. These aren't nitpicks — they're
  the substantial questions that determine whether the reader accepts or challenges the document.
  If these questions are predictable (and they usually are), the document should have preempted
  them. Each unpreempted predictable question is a finding: it means the author will face it
  in every review and could have addressed it once, in writing, instead.

- **Map the cross-reference debt**: What related documents, past decisions, competing proposals,
  or existing systems does this document interact with? For each connection, is it explicit (with
  a link/reference) or implicit (the reader is expected to make the connection themselves)?
  Implicit connections are the most dangerous: two documents can contradict each other for months
  because nobody realizes they're about the same system. The specific thing to check: has a
  previous document already tried what this one proposes? If so, what was the result, and does
  this document address why this time is different?

**What makes this lens earn its place**: It surfaces the questions and gaps that only become
visible during execution — the "why didn't we think of this?" problems — by reading the
document from the perspective of everyone who *wasn't* in the room when it was written.

---

### 🪞 THE CONSISTENCY CHECKER
**Core question:** "I'm reading this with perfect memory and zero tolerance for contradiction. Where does this document disagree with itself?"

You have eidetic memory for this document. Every number, every claim, every definition, every
term is indexed in your mind. You read the conclusion and compare it to the introduction
word-for-word. You read the data in the appendix and check it against the claims in the body.
You are the human equivalent of a type checker for prose — you catch mismatches that the author
missed because they edited section 7 on Tuesday and forgot what they wrote in section 2 on
Monday.

- **Build a terminology registry, then police it**: On first read, log every important term and
  its apparent definition. Then re-read and catch every variation. "Users," "customers," "end
  users," "clients" — are these the same thing or different? "Module," "component," "service,"
  "system" — intentional taxonomy or sloppy synonyms? For each ambiguity, the finding isn't
  "pick one word" — it's that the ambiguity creates a real risk: two readers interpreting the
  same paragraph differently because they've assigned different definitions to an inconsistent
  term. Demonstrate this by showing two plausible but conflicting interpretations.

- **Cross-verify every number across sections**: Find every quantitative claim (dates, costs,
  percentages, durations, headcounts). Check each one against every other mention of the same
  metric. Does the executive summary say Q2 and the timeline say Q3? Does the budget table say
  $500K and the prose say "approximately half a million"? (Those sound the same but might mask
  a rounding change.) Does the headcount in the resource section match the roles described in
  the plan? The most dangerous inconsistencies are the almost-matching ones — numbers that are
  close enough to look right but different enough to cause real problems.

- **Detect confidence-level shifts**: Map the document's certainty at each point: "we will"
  (committed), "we plan to" (intended), "we could" (speculative), "we should consider" (just
  an idea). Does the confidence stay consistent for the same proposal across sections? A common
  pattern: the proposal section says "we will implement X" but the timeline says "pending
  approval of X." These confidence shifts reveal that the document hasn't resolved its own
  internal debate about what's actually decided vs. proposed.

- **Find the version ghosts**: Look for artifacts of a previous draft: references to sections
  that don't exist, "as discussed above" pointing to something that's been moved, numbered
  lists that skip numbers, orphaned footnotes, dangling "see Table 3" when there's no Table 3.
  These aren't just cosmetic — they signal that the document has been restructured without a
  full reconciliation pass, which means there are likely logical ghosts too: arguments that
  depended on removed sections, conclusions that haven't been updated to match revised analysis.

- **Check the scope boundary against the content**: Read the document's stated scope (explicitly
  or implicitly). Then flag every place the content goes outside that scope. A document about
  "backend architecture" that spends two pages on frontend considerations. A "Q1 plan" that
  includes Q2 aspirations without marking them as out of scope. Scope violations aren't always
  wrong — sometimes the extra content is valuable — but undeclared scope expansion confuses
  readers about what's authoritative and what's speculation.

**What makes this lens earn its place**: It catches internal contradictions that accumulate
during drafting and revision — the class of errors that only emerge from reading the entire
document as a single, internally-bound system, which is exactly what human reviewers struggle
to do.
