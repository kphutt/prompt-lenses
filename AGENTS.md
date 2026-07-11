# prompt-lenses — Conventions

## Structure

```
core/           ← The intellectual property. Model-agnostic lenses and fragments.
  template/     ← The structural spec every lens inherits (Phase 2.1 — done)
  fragments/    ← Shared components composed into every lens (Phase 2.2 — next)
  mandatory/    ← Lenses that run on every review (Security, Privacy, etc.)
  standard/     ← Optional lenses by domain (code/ and doc/)
  custom/       ← User-generated lenses for novel artifact types
meta/           ← Meta-prompts that generate and validate lenses
platforms/      ← Thin wrappers that adapt lenses to specific AI platforms
research/       ← Research outputs and the prompts that produced them
docs/           ← Decision records and design brainstorms
scripts/        ← Build tooling (e.g., fragment assembly)
```

## Conventions

- **Lenses are cognitive modes, not checklists.** Each lens changes HOW the model thinks.
- **Each lens gets its own `.md` file.** Independently excellent, independently updatable.
- **Core is model-agnostic.** No platform-specific formatting in `core/`. Platform stuff lives in `platforms/`.
- **Fragments compose, not copy-paste.** `{{fragment:name}}` markers are replaced at build time.
- **XML tags for section boundaries, markdown inside.** The hybrid standard across Claude and GPT.
- **Positive framing.** "Do X" not "Don't do Y" — except for `<out_of_scope>` and safety constraints.

## Key Files

- `plan.md` — Single source of truth for the project. All design decisions live here.
- `core/template/lens-template.md` — The skeleton every lens inherits. Read this before writing any lens.
- `ROADMAP.md` — Prioritized backlog of next steps.

## Docs

This project follows the project-docs convention: `ROADMAP.md` for big rocks, `docs/decisions/` for decision records.
