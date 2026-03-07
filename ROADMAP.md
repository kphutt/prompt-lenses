# Roadmap

<!-- Prioritized big rocks. This is the backlog. -->

## Next Up

- [x] **Phase 2.2** — Design shared fragments (`core/fragments/`)
- [x] **Phase 3** — Finalize mandatory lens rosters (5 code + 6 doc)
- [ ] **Phase 4** — Build mandatory lenses (11 total)

## Later

- [ ] **Phase 5** — Rebuild standard lenses on the new template
- [ ] **Phase 6** — Platform wrappers (Claude, Gemini, generic)
- [ ] **Phase 7** — promptfoo evaluation framework
- [ ] **Phase 8** — Meta-prompt maintenance
- [ ] **Persona prompt templates** — Reusable expert persona prompts (Rob Pike, Casey Muratori, Martin Fowler, etc.) for design review. Each persona has a concrete identity, specific critique questions, and a requirement to return numbered actionable recommendations. Emerged from text-adventure-v2 combat initiative planning.
- [ ] **Idiom Analyst lens** — Language-specific design pattern review. Instead of generic "is this correct?", asks "does this match how this language/ecosystem solves this problem?" Covers Go idioms, React patterns, Python conventions, etc.
- [ ] **Conflict Resolution fragment** — Composable fragment for multi-reviewer workflows. When multiple lenses produce conflicting recommendations: identify the conflict, articulate why each side is right in its frame, find a synthesis or document the tradeoff.
- [ ] **The Catalyst** — Three-stage pipeline prompt that finds the single highest-leverage change to any artifact, or says nothing. Stage 1 (Backcast) is fast and frequent — envision the ideal, measure the gap. Stage 2 (Diagnose) classifies the gap as structural, framing, or both. Stage 3 produces exactly one transformative idea with runner-ups. First pipeline in prompt-lenses (not a lens). Core prompt lives in `core/pipelines/catalyst.md`; ai-toolkit wraps it as `/catalyst` skill. See [brainstorm](docs/design/catalyst/brainstorm.md).

See `plan.md` for full details and dependencies.
