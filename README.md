# prompt-lenses

A personal library of high-quality, model-agnostic prompts ("lenses") for reviewing code and documents through distinct cognitive perspectives.

Each lens is a fully realized analytical mode — not "check for X" but a complete reorientation of what you're looking for, what questions you're asking, and what "good" looks like.

## The Idea

Investing heavily in prompt quality produces compounding returns. The models get better, but better models with better prompts pull even further ahead.

Lenses are built on a [shared template](core/template/lens-template.md) with an 8-element structure (Identity → Mission & Scope → Criteria → Methodology → Output Format → Examples → Edge Cases → Closing Anchor) and validated against a 6-test quality framework. They compose shared fragments for output format, severity ratings, and anti-padding rules.

## Status

**Early development.** Research complete, template designed, building lenses next.

See [plan.md](plan.md) for the full project plan and [ROADMAP.md](ROADMAP.md) for what's next.

## Structure

```
core/           Lenses, template, and fragments (model-agnostic)
meta/           Meta-prompts that generate and validate lenses
platforms/      Thin wrappers for Claude, Gemini, etc.
research/       Research outputs and the prompts that produced them
```

## License

Personal project. Not yet licensed for distribution.
