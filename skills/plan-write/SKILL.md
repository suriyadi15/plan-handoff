---
name: plan-write
description: Persists a plan (implementation plan, plan-of-action, or planning output) into a self-contained Markdown document under ~/.plans/ so it can be handed off to and executed by a fresh AI agent CLI session. Use this whenever the user asks to create/write/draft a plan (e.g. "plan an implementation", "write a roadmap"), finishes planning and wants to save it, or wants the plan saved for another agent to execute — even if they don't explicitly say "save to file" or "handoff".
---

# Plan Write

Turn a planning result into a standalone Markdown document at `~/.plans/`, so a
different AI agent CLI can open it and immediately execute the steps.

## Input

The topic may come from a slash invocation (`/plan-write <topic>`) or from the
user's message. If neither gives a topic, use the planning result already in the
conversation, or ask what the plan is about.

## When to apply

- The user asks to create / write / draft a plan, roadmap, or implementation steps.
- The user has just finished planning and wants it saved.
- The user wants to hand the plan to another CLI / session for execution.

## Where to save

- Folder: `~/.plans/` (create it if it doesn't exist).
- Filename: `<YYYY-MM-DD>_<topic-slug>.md` — lowercase, words separated by `-`.
  Example: `~/.plans/2026-11-20_add-login-feature.md`.

## Template — ALWAYS use this exact structure

```
# [Plan title]

## Goal
One or two sentences on what should be achieved.

## Context
Background: repository, starting state, constraints, and anything the executor
must know. Be concrete — name repos, directories, and files.

## Steps
- [ ] 1. First step (specific + concrete file path)
- [ ] 2. Next step
- [ ] 3. ...

## Files / Areas affected
- `path/to/file` — the planned change

## Acceptance criteria
- [ ] How to verify the plan succeeded

## Dependencies / Notes
Dependencies, risks, and key decisions the executor should respect.
```

## Writing rules (why these matter)

- **Self-contained**: the executor has none of your conversation context, so the
  document must stand alone. Spell out everything needed to act.
- **Ordered, specific, actionable**: steps in execution order, with concrete
  file paths.
- Use `- [ ]` checkboxes so the executor can tick off progress.
- After writing, report the full path, e.g. `~/.plans/2026-11-20_add-login-feature.md`.
