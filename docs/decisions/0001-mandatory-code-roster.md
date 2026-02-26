# Decision Record: Mandatory Code Lens Roster

**Status:** Accepted
**Date:** 2026-02-25
**Phase:** 3 (Decide)

## Context

Phase 2.2 (fragments) is complete. Before building mandatory lenses in Phase 4, we need to
finalize which lenses are mandatory and in what order they run. The current proposal is 5
mandatory code lenses. Three new candidates (Bug Finder, Smooth Handoff, Toil Detector) were
evaluated and rejected for mandatory status. Three overlap questions (Adversary/Security,
Editor/Plain Language, Operator/Failure Modes) were resolved — all pairs stay separate.

## Decision

### The 5 Mandatory Code Lenses

| # | Lens | Cognitive Mode | Sequence Phase | Sequence Position |
|---|------|---------------|----------------|-------------------|
| 1 | **Security** | Trace data flows and check controls — systematic analysis of exploit surfaces | analytical | 3 |
| 2 | **Privacy** | Track data lifecycle — where personal data enters, moves, persists, and exits | analytical | 4 |
| 3 | **Testability** | Apply the "falsifiable check" standard — can every claim be proven or disproven? | analytical | 8 |
| 4 | **Plain Language** | Rewrite at the lexical level — concrete nouns, vivid verbs, sentence-level clarity | detail | 11 |
| 5 | **Failure Modes** | Map what goes wrong abstractly — what breaks, what cascades, what's the blast radius | analytical | 5 |

### Full Code Sequence (mandatory marked with *)

1. Deleter (structural)
2. Flow Analyst (structural)
3. *Security (analytical)
4. *Privacy (analytical)
5. *Failure Modes (analytical)
6. Operator (analytical)
7. Specification Lawyer (analytical)
8. *Testability (detail)
9. Time Traveler (detail)
10. Newcomer (detail)
11. *Plain Language (detail)

### Scope Boundary Notes

Each mandatory lens's `<out_of_scope>` should reference the 2-3 most likely sources of
overlap from the mandatory set. Designed as a set:

- **Security** references: Privacy (data lifecycle is Privacy's job), Testability (provability
  is Testability's job), Plain Language (naming clarity is Plain Language's job), Failure Modes
  (abstract failure mapping is Failure Modes' job)

- **Privacy** references: Security (exploit surfaces are Security's job), Plain Language
  (policy wording clarity is Plain Language's job), Failure Modes (what happens when privacy
  controls fail is Failure Modes' job)

- **Testability** references: Security (whether tests cover security cases is Security's job),
  Failure Modes (whether failure paths are covered is Failure Modes' job), Plain Language
  (whether test names are clear is Plain Language's job)

- **Plain Language** references: Security (whether security terms are accurate is Security's
  job), Testability (whether specifications are verifiable is Testability's job), Privacy
  (whether privacy disclosures are complete is Privacy's job)

- **Failure Modes** references: Security (whether failures create exploits is Security's job),
  Privacy (whether failures leak data is Privacy's job), Testability (whether failure paths
  are testable is Testability's job)

### Standard Lens Overlap Resolution (Code)

- **Adversary stays separate from Security.** Adversary chains observations into attack
  narratives (creative composition). Security traces data flows and checks controls (systematic
  analysis). Adversary's `<out_of_scope>` references Security for individual vulnerability
  cataloging.

- **Operator stays separate from Failure Modes.** Operator simulates a 3AM incident (can I
  diagnose and fix this?). Failure Modes maps what goes wrong abstractly (what breaks, what's
  the blast radius?). Operator's `<out_of_scope>` references Failure Modes for abstract
  failure analysis.

### Candidates Evaluated and Deferred

- **Bug Finder** — Overlaps with Scientist (code) and Consistency Checker (doc). Its "trace
  execution" mode is distinct but not universal. Standard lens, evaluated in Phase 5.
- **Smooth Handoff** — Distinct but niche. Standard doc lens, possibly code variant for API
  ergonomics. Evaluated in Phase 5.
- **Toil Detector** — Genuinely novel mode but not universal enough. Standard lens, evaluated
  in Phase 5.

## Consequences

- Phase 4 builds 5 mandatory code lenses (4.1, 4.3, 4.5, 4.7, 4.9)
- Each lens is built with scope boundaries referencing sibling mandatory lenses by name
- Standard code lenses (Adversary, Operator, etc.) are rebuilt in Phase 5 with explicit
  `<out_of_scope>` referencing the mandatory lens they're most likely to overlap with
- The code mandatory set is smaller than the doc set (5 vs 6) — this asymmetry is intentional
  because Connector's "what's missing?" mode serves a structural gap unique to documents
