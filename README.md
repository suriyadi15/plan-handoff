# plan-handoff

A pair of skills to **write a plan** in one agent CLI, then **execute it** in
another.

> **Flow:** CLI 1 creates a plan → saved to `~/.plans/<date>_<topic>.md` →
> CLI 2 (a fresh session) opens and executes that plan.

## Skills

| Skill | Role | Direction |
|---|---|---|
| [`plan-write`](./plan-write/SKILL.md) | Writes a plan and saves it to `~/.plans/` | CLI 1 (planning) |
| [`plan-execute`](./plan-execute/SKILL.md) | Reads a plan and carries out its steps | CLI 2 (execution) |

Plans use a standard template — **Goal, Context, Steps, Files, Acceptance
criteria, Dependencies** — with `- [ ]` checkboxes so progress can be ticked off.

## Install the skills

### Via `npx skills` (cross-CLI)

```bash
npx skills add suriyadi15/plan-handoff@plan-write
npx skills add suriyadi15/plan-handoff@plan-execute
```

### Manual

Copy each skill folder into your CLI's skills directory:

```bash
# Claude Code
cp -r plan-write ~/.claude/skills/plan-write
cp -r plan-execute ~/.claude/skills/plan-execute

# OpenCode
cp -r plan-write ~/.agents/skills/plan-write
cp -r plan-execute ~/.agents/skills/plan-execute
```

## Install the slash commands

Slash commands aren't shipped by `npx skills`, so copy them manually:

```bash
# Claude Code
cp commands/claude/plan-write.md ~/.claude/commands/plan-write.md
cp commands/claude/plan-execute.md ~/.claude/commands/plan-execute.md

# OpenCode
cp commands/opencode/plan-write.md ~/.config/opencode/commands/plan-write.md
cp commands/opencode/plan-execute.md ~/.config/opencode/commands/plan-execute.md
```

## Usage

**1. CLI 1 — write a plan**

```
/plan-write login feature
```

You can also just ask naturally ("create a plan for the login feature"). The
`plan-write` skill saves the plan to
`~/.plans/2026-11-20_add-login-feature.md`.

**2. CLI 2 (new) — execute the plan**

```
/plan-execute ~/.plans/2026-11-20_add-login-feature.md
```

The `plan-execute` skill reads the plan, carries out each step in order, ticks
`- [x]` in the file, and reports a summary.

## Codex / Gemini CLI

`SKILL.md` is the cross-agent standard (supported by Claude Code, OpenCode,
Cursor, and the `skills.sh` ecosystem). For Codex CLI (`AGENTS.md`) and Gemini
CLI (its own extension format), the skill content is generic and can be pasted /
adapted manually — there is no auto-install.
