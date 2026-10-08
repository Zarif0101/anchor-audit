# anchor-audit

A Claude skill that makes content for my own brand read like a specific person made it. Built and stress-tested with Simulation Lab v2 on 2026-10-08.

- **Lite** (default): draft, then one patch-only audit pass against AI tells.
- **Anchor** (opt-in): up to 3 intake questions, I type one real line, Claude builds around it and never edits it.

## Install
1. Download this repo as a ZIP, or zip the folder with `SKILL.md` at the top level.
2. Upload it in Claude: Settings → Capabilities → Skills.
3. Copy `state-template/anchor-audit-state/` into a folder connected to Cowork. The skill folder is read-only, so state lives there.
4. Run `eval/step0.md` (30 min) before relying on it.

## Layout
```
SKILL.md                 entry point: scope, six moves, modes
references/audit.md      patch-only audit procedure + move bank
references/tells.md      AI-tell catalogue (audit step only)
references/intake-bank.md
references/text.md | design.md | video.md | code.md
eval/step0.md            self-test and kill rules
state-template/          voice corpus, log, last-moves (copy out)
docs/run-report.md       the Simulation Lab report behind the design
```
