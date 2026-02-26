# Decision Record: Mandatory Doc Lens Roster

## Status

Accepted — 2026-02-25, Phase 3 (Decide)

## Context

Phase 2.2 (fragments) is complete. Before building mandatory lenses in Phase 4, we need to
finalize which lenses are mandatory and in what order they run. The doc set adds one lens
beyond the shared 5: Connector, whose "what's missing?" cognitive mode caught a class of
failures no other lens found during Phase 2.2 dogfooding. This makes the mandatory sets
asymmetric (5 code, 6 doc) — intentionally, because the cognitive needs differ by domain.

## Decision

### The 6 Mandatory Doc Lenses

| # | Lens | Cognitive Mode | Sequence Phase | Sequence Position |
|---|------|---------------|----------------|-------------------|
| 1 | **Connector** | Identify structural gaps — what's missing, what's out of sequence, what doesn't link | structural | 2 |
| 2 | **Security** | Trace security implications in document content — are risks identified and addressed? | analytical | 4 |
| 3 | **Privacy** | Track privacy implications — are data handling, consent, and retention addressed? | analytical | 5 |
| 4 | **Testability** | Apply the "falsifiable check" standard — can every claim be verified or measured? | analytical | 6 |
| 5 | **Failure Modes** | Map what happens when this document's guidance fails — gaps, wrong assumptions, cascades | analytical | 7 |
| 6 | **Plain Language** | Rewrite at the lexical level — concrete nouns, vivid verbs, sentence-level clarity | detail | 11 |

### Full Doc Sequence (mandatory marked with *)

1. Executive (structural)
2. *Connector (structural)
3. Skeptic (analytical)
4. *Security (analytical)
5. *Privacy (analytical)
6. *Testability (analytical)
7. *Failure Modes (analytical)
8. Outsider (detail)
9. Consistency Checker (detail)
10. Editor (detail)
11. *Plain Language (detail)

### Why Connector Is Mandatory for Docs

During Phase 2.2 dogfooding, the Connector's "what's missing?" mode identified structural
gaps that no other lens caught — specifically, missing links between sections, absent
prerequisites, and logical sequencing failures. For code, the structural gap is covered by
Flow Analyst (data architecture) and Deleter (is this worth keeping?). For docs, no standard
lens fills this role. The Connector is the only lens whose primary question is "what isn't
here that should be?"

### Scope Boundary Notes

Each mandatory lens's `<out_of_scope>` should reference the 2-3 most likely sources of
overlap from the mandatory set. Designed as a set:

- **Connector** references: Plain Language (whether individual sentences are clear is Plain
  Language's job), Testability (whether claims are verifiable is Testability's job), Security
  (whether security sections are present is Security's job — Connector flags missing sections,
  Security evaluates their content)

- **Security** references: Privacy (data lifecycle is Privacy's job), Testability (provability
  is Testability's job), Connector (structural completeness is Connector's job), Failure Modes
  (abstract failure mapping is Failure Modes' job)

- **Privacy** references: Security (threat modeling is Security's job), Plain Language (policy
  wording clarity is Plain Language's job), Failure Modes (what happens when privacy controls
  fail is Failure Modes' job)

- **Testability** references: Security (whether tests cover security cases is Security's job),
  Failure Modes (whether failure paths are covered is Failure Modes' job), Connector (whether
  the document structure supports verification is Connector's job)

- **Failure Modes** references: Security (whether failures create vulnerabilities is Security's
  job), Privacy (whether failures leak data is Privacy's job), Testability (whether failure
  paths are verifiable is Testability's job)

- **Plain Language** references: Connector (whether sections are present is Connector's job),
  Testability (whether specifications are verifiable is Testability's job), Privacy (whether
  privacy disclosures are complete is Privacy's job)

### Standard Lens Overlap Resolution (Doc)

- **Editor stays separate from Plain Language.** Editor is structural (cut 40% with zero
  meaning loss). Plain Language is lexical (concrete nouns, vivid verbs, sentence-level
  clarity). Different cognitive levels. Editor's `<out_of_scope>` references Plain Language
  for word-level rewriting.

### Candidates Evaluated and Deferred

- **Bug Finder** — Doc variant would find factual errors, dead references, unimplementable
  specs. Overlaps with Consistency Checker. Standard lens, evaluated in Phase 5.
- **Smooth Handoff** — Distinct from Outsider (comprehension) and Connector (completeness).
  Standard doc lens, evaluated in Phase 5.
- **Toil Detector** — Challenges what must be manual. Standard lens, evaluated in Phase 5.

## Consequences

- Phase 4 builds 6 mandatory doc lenses (4.2, 4.4, 4.6, 4.8, 4.10, and new 4.11 for
  connector-doc.md)
- Connector is doc-only mandatory — no code variant in the mandatory set
- Each lens is built with scope boundaries referencing sibling mandatory lenses by name,
  including Connector for the doc variants
- The doc mandatory set is larger than code (6 vs 5) — this asymmetry is intentional
- `core/mandatory/connector-doc.md` is added to the file structure
