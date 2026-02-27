# prompt-lenses

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

A prompt library for reviewing code and documents through distinct cognitive perspectives.

## The Idea

Most review prompts are checklists — "check for security issues," "check for performance problems." Lenses are different: each one is a complete cognitive reorientation that changes what you notice, what questions you ask, and what "good" looks like.

A checklist says *"check for security vulnerabilities."* A lens says:

> You are a creative, patient attacker. You don't run scanners — you *read* code and think about what the author assumed but never enforced. Your art is finding the gap between what the code *should* reject and what it *actually* rejects, then chaining those gaps into something devastating.

The difference: a checklist scans for known patterns. A lens adopts a cognitive mode that surfaces findings the reviewer wouldn't have looked for.

## Influences

[Six Thinking Hats](https://en.wikipedia.org/wiki/Six_Thinking_Hats) (perspective sequencing), [ATAM](https://en.wikipedia.org/wiki/Architecture_tradeoff_analysis_method) (architectural tradeoff analysis), multi-pass editing from publishing (macro-to-micro sequencing), [thibaultyou/prompt-library](https://github.com/thibaultyou/prompt-library) (confidence scoring and abstention).

## Status

Research complete — landscape survey, prompt anatomy study, 30 design decisions recorded. [Template](core/template/lens-template.md) and shared [fragments](core/fragments/) built. Zero lenses built yet.

## Structure

```
core/           Template, fragments, and draft lens definitions
research/       Landscape survey, prompt anatomy study
meta/           Quality framework, roster definitions
docs/           Design decisions
platforms/      Platform-specific wrappers (placeholder)
```

## License

MIT
