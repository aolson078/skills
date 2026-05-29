# Alex Olson Voice Skill Package

This folder is a reusable voice/style package for AI agents.

## How to use

Give the whole folder to an agent if it supports multi-file skills, knowledge packs, repositories, or project context.

Recommended loading order:

1. `SKILL.md`
2. `voice_profile.md`
3. `style_rules.md`
4. `context_adaptation.md`
5. `examples.md`
6. `source_inventory.md`
7. `prompt.md`

For agents that only accept one prompt, use `prompt.md`.

## Design principle

`SKILL.md` tells the agent how to use the skill. `voice_profile.md` defines the voice. The other files constrain, adapt, or support the voice.

The package intentionally separates:

- Core voice traits.
- Operational writing rules.
- Context-specific adaptation.
- Examples.
- Source provenance.
- Compact fallback prompt.

This is meant to reduce overfitting and keep agents from treating all style guidance as equally important.
