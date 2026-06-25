---
name: agent-qa-red-team
description: Run read-only QA and red-team reviews for serious agent work, code changes, docs, releases, memory edits, and automation; use to find bugs, hallucinated claims, security/privacy issues, missing validation, weak reasoning, and overclaimed completion before finalizing.
---

# Agent QA / Red Team

Use this skill when serious work deserves an independent read-only second pass before the hub claims it is done.

The reviewer is not a co-author. The reviewer finds actionable problems, missing evidence, and release-blocking risks. Findings come first. Summaries are secondary.

## Default Posture

- Read-only unless the hub explicitly promotes the lane.
- Findings before praise.
- Evidence over vibes.
- Reproduction over speculation.
- Blockers are named plainly.
- Low-confidence risks are separated from high-confidence findings.
- Secrets are reported by path/type only, never pasted.

## Review Workflow

1. **Define review scope**
   - Identify changed files, commits, diffs, docs, generated artifacts, commands, screenshots, or claims to review.
   - State what is out of scope.
   - Confirm whether the review is for code, docs, security/privacy, validation, reasoning, release, memory, or mixed work.

2. **Choose reviewer roles**
   Use the smallest useful set:
   - `Code QA`: bugs, edge cases, regressions, maintainability, tests.
   - `Docs QA`: incorrect claims, missing diagrams/links, stale instructions, poor handoff.
   - `Security/Privacy`: secrets, credential handling, auth, external actions, data exposure.
   - `Validation QA`: missing, weak, skipped, or misleading tests/builds/checks.
   - `Reasoning Red Team`: unsupported assumptions, hallucinated facts, overconfident claims, bad scope decisions.
   - `Release QA`: dirty worktrees, branch state, CI/deploy status, versioning, pushed commits.
   - `Memory QA`: durable memory quality, privacy, bloat, and whether the note belongs in daily or long-term memory.

3. **Inspect evidence**
   - Prefer `git diff`, `git status`, logs, generated files, and exact commands.
   - Use file and line references for code/docs findings when possible.
   - Use command output or reproduction steps for behavioral findings.
   - If evidence is missing, report the missing evidence instead of inventing confidence.

4. **Classify findings**
   Use these levels:
   - `blocker`: should stop release/final claim.
   - `high`: likely bug, security/privacy risk, or serious user-visible failure.
   - `medium`: meaningful correctness, validation, maintainability, or handoff issue.
   - `low`: polish or small clarity issue.
   - `question`: needs hub/user decision.
   - `risk`: plausible but low-confidence concern.

5. **Write findings**
   Each finding must include:
   - severity
   - title
   - evidence
   - impact
   - recommendation
   - confidence

   For file-based findings, include:
   - file
   - line or range when known

6. **Report in review order**
   Report format:
   - Blockers
   - Findings
   - Questions
   - Low-confidence risks
   - Validation gaps
   - Summary

   If there are no findings, say so clearly and name residual test gaps or risk.

7. **Hub decision**
   The hub verifies the review and decides whether to:
   - fix now
   - defer with rationale
   - ask the user
   - rerun validation
   - stop the release

## Reviewer Contract

Return:

- `status`: done, blocked, partial, or no-findings
- `scope`: what was reviewed
- `findings`: prioritized list
- `questions`: decision points
- `validation_gaps`: checks not run or weak evidence
- `risks`: low-confidence concerns
- `summary`: short synthesis only after findings
- `handoff`: exact next action for the hub

## CLI

Use the bundled script when a review lane returns structured findings and the hub wants a clean report:

```bash
python3 scripts/agent_qa_red_team.py validate findings.json
python3 scripts/agent_qa_red_team.py report findings.json --out review.md
```

The script validates required fields, sorts findings by severity, and writes a concise Markdown report.

## Read-Only Rules

- Do not edit files during a review lane.
- Do not stage, commit, push, deploy, publish, or send messages.
- Do not run destructive commands.
- Avoid commands that mutate lockfiles, caches, or generated outputs unless the hub explicitly asks for a tester lane.
- For secret findings, report the file path and secret type only.

## Validation Claims

Challenge validation claims when:

- tests were not run
- generated files were not checked after generation
- CI status was not inspected after push
- screenshots or visual output were not verified for UI work
- docs were regenerated but drift checks were skipped
- a command failed but the final report hides it
- a release was claimed before publication/deploy evidence existed

## Overclaim Detection

Flag overclaims when the final answer says:

- shipped, deployed, applied, published, fixed, or validated without evidence
- no issues found while scope was partial
- "all" when only a subset was checked
- "safe" without explaining risk boundary
- "latest" or "current" without time-sensitive verification

## Role References

Read `references/reviewer-roles.md` when assigning a specialized review lane or writing a subagent brief.
