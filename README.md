# plan-handoff

Two agent skills to **write a plan** in one AI coding CLI, then **execute it**
in another.

```
CLI 1 (plan-write)  ──►  ~/.plans/<date>_<topic>.md  ──►  CLI 2 (plan-execute)
```

| Skill | What it does |
|---|---|
| [`plan-write`](./skills/plan-write/SKILL.md) | Saves a plan as a self-contained Markdown file in `~/.plans/` |
| [`plan-execute`](./skills/plan-execute/SKILL.md) | Reads a plan file, runs its steps in order, ticks `- [x]` as it goes |

Plans use a fixed template: **Goal, Context, Steps, Files, Acceptance criteria,
Dependencies**, with `- [ ]` checkboxes for progress.

## Install

One command:

```bash
npx skills add suriyadi15/plan-handoff
```

The [skills CLI](https://github.com/vercel-labs/skills) then shows two checklists:

1. **Which skills** — `plan-write`, `plan-execute` (or both).
2. **Which agents** — tick any of Claude Code, OpenCode, Codex, Cursor, Gemini CLI
   and 40+ others. The skills are copied to the right folder for each.

Then choose scope: **project** (this repo only) or **global** (all projects).

### Skip the prompts

```bash
# Both skills, global, Claude Code + OpenCode, no questions
npx skills add suriyadi15/plan-handoff -g -a claude-code -a opencode -y

# Every agent
npx skills add suriyadi15/plan-handoff --agent '*' -g -y

# Only one skill
npx skills add suriyadi15/plan-handoff --skill plan-write

# Just list what is inside
npx skills add suriyadi15/plan-handoff --list
```

### Find, update, remove

```bash
npx skills find plan-handoff     # search for skills
npx skills update                # update installed skills
npx skills remove plan-write     # uninstall
```

### Manual install

Copy the folders yourself if you prefer:

```bash
cp -r skills/* ~/.claude/skills/   # Claude Code
cp -r skills/* ~/.agents/skills/   # OpenCode, Codex and other .agents-compatible CLIs
```

## Usage

**1. In CLI 1 — write the plan**

| Agent | How |
|---|---|
| Claude Code | `/plan-write login feature` |
| Others | Ask: *"write a plan for the login feature"* |

Result: `~/.plans/2026-11-20_add-login-feature.md`. The path is printed when done.

**2. In CLI 2 (new session) — execute it**

| Agent | How |
|---|---|
| Claude Code | `/plan-execute ~/.plans/2026-11-20_add-login-feature.md` |
| Others | Ask: *"execute the plan ~/.plans/2026-11-20_add-login-feature.md"* |

With no path given, `plan-execute` lists the plans in `~/.plans/` and asks which
one to run. It does each step in order, ticks `- [x]` in the file, checks the
acceptance criteria, and reports a summary. If a step is blocked it stops and
asks instead of guessing.

## Repo layout

```
skills/
├── plan-write/SKILL.md
└── plan-execute/SKILL.md
```

`skills/<name>/SKILL.md` is the layout the skills CLI auto-discovers.
