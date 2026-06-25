# Agent QA / Red Team

Reusable read-only review workflow for serious agent work.

This skill gives the hub a sharper second pass before claiming work is done: bugs, regressions, hallucinated claims, missing validation, security risks, privacy leaks, and weak reasoning should be caught as findings with evidence.

## What It Does

- Defines read-only reviewer roles for code, docs, security, validation, and reasoning
- Provides review checklists and a structured finding schema
- Prioritizes findings before summaries
- Requires file/line evidence, logs, commands, or reproducible steps
- Separates blockers, findings, questions, and low-confidence risks
- Produces concise reports the hub can act on

## Quick Start

Create a Markdown review report from a findings JSON file:

```bash
python3 scripts/agent_qa_red_team.py report examples/findings-example.json --out /tmp/qa-report.md
```

Validate a findings file without writing a report:

```bash
python3 scripts/agent_qa_red_team.py validate examples/findings-example.json
```

## Skill Contents

- `SKILL.md` - review workflow and reviewer contract
- `scripts/agent_qa_red_team.py` - findings validator and report generator
- `templates/` - review brief, findings schema, checklist, and report template
- `references/reviewer-roles.md` - role-specific review prompts
- `examples/findings-example.json` - sample findings input
- `docs/` - generated documentation

## Safety

Review lanes are read-only by default. They do not edit files, fix issues, run destructive commands, publish, push, send messages, or expose secrets.
