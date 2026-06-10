---
description: Draft, rewrite, summarize, or review prose in Alex Olson's voice.
argument-hint: "[draft|rewrite|summarize|review] <text, file path, audience, or goal>"
allowed-tools: [Read, Grep, Glob, Task]
---

# Alex Voice

Use this command as the fast path for writing in Alex Olson's voice.

User request:

$ARGUMENTS

## Instructions

1. Determine whether the user wants a draft, rewrite, summary, edit, critique, or voice check.
2. If the request references files, read only the relevant file content before writing.
3. Load the skill: `SKILL.md`, `voice_profile.md`, `style_rules.md`, the matching section of `context_adaptation.md`, and the matching samples from `examples.md`. If context is tight, use `prompt.md` alone.
4. Preserve facts, required structure, audience fit, and technical meaning before applying style.
5. Do not invent Alex's personal experiences, credentials, relationships, or biographical facts.
6. Do not add corporate hype, exaggerated enthusiasm, or generic AI phrasing.
7. Run the Final voice check from `SKILL.md` and fix any failures before returning.
8. Return the finished prose first unless the user explicitly asks for notes or critique.

## Output Shape

- For `draft`, `rewrite`, `edit`, or unspecified requests: return the finished text only.
- For `review` or `critique`: use `Strongest fit`, `Misses`, and `Suggested revision`.
- For `summarize`: keep facts tight; use Alex's voice in framing rather than embellishment.
- If a meaningful assumption or tradeoff affected the result, add a short `Note` after the prose.
