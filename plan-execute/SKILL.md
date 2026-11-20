---
name: plan-execute
description: Executes a saved plan document (a Markdown file, typically under ~/.plans/ or any path the user provides) by working through its steps in order, ticking off completed tasks, and updating the plan file with progress. Use this whenever the user points at a plan file, says "execute" or "run" this plan, or asks to carry out a saved plan document step by step.
---

# Plan Execute

Read a saved plan document and execute it to completion, so a fresh CLI session
can carry out a plan written earlier by another agent.

## When to apply

- The user gives a path to a `.md` plan file and asks to execute it.
- The user says "execute" or "run" a plan.
- The user opens a plan document and wants it carried out.

## How to execute

1. Read the plan file.
2. Understand each section:
   - **Goal** — the outcome to achieve.
   - **Context** — starting state and constraints.
   - **Steps** — the ordered tasks to perform.
   - **Files / Areas affected** — what to touch.
   - **Acceptance criteria** — how to verify success.
   - **Dependencies / Notes** — risks and dependencies.
3. Execute the steps in order. For each step:
   - Do the actual work (edit files, run commands, etc.).
   - Mark the step's checkbox `- [x]` in the plan file once done.
4. After all steps, verify against the acceptance criteria.
5. Report a short summary: what was done, what remains, and any deviations.

## Rules (why these matter)

- Follow the plan's order. Don't silently skip a step: if one is blocked or needs
  a decision, stop and ask the user instead of guessing.
- Update the plan file's checkboxes as you go, so progress stays visible to
  anyone (or any agent) that reopens it.
- Keep the plan's other sections intact; only tick off steps and optionally add a
  short progress note.
