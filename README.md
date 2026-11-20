# plan-handoff

Sepasang skill untuk **menulis plan** di satu agent CLI, lalu **mengeksekusinya** di agent CLI lain.

> **Alur:** CLI 1 membuat plan → tersimpan ke `~/.plans/<tanggal>_<topik>.md` → CLI 2 (sesi baru) membuka & mengeksekusi plan itu.

## Skill

| Skill | Peran | Arah |
|---|---|---|
| [`plan-write`](./plan-write/SKILL.md) | Menyusun plan & menyimpannya ke `~/.plans/` | CLI 1 (planning) |
| [`plan-execute`](./plan-execute/SKILL.md) | Membaca plan & mengerjakan langkah-langkahnya | CLI 2 (eksekusi) |

Plan disimpan memakai template standar: **Tujuan, Konteks, Langkah-langkah, Files, Kriteria Selesai, Catatan** — dengan checkbox `- [ ]` agar progres bisa dicentang.

## Install skill

### Via `npx skills` (lintas CLI)

```bash
npx skills add <owner>/plan-handoff@plan-write
npx skills add <owner>/plan-handoff@plan-execute
```

Ganti `<owner>` dengan username GitHub-mu.

### Manual

Copy folder skill ke direktori skills CLI-mu:

```bash
# Claude Code
cp -r plan-write ~/.claude/skills/plan-write
cp -r plan-execute ~/.claude/skills/plan-execute

# OpenCode
cp -r plan-write ~/.agents/skills/plan-write
cp -r plan-execute ~/.agents/skills/plan-execute
```

## Install slash command `/eksekusi`

Slash command tidak ikut `npx skills`, jadi copy manual:

```bash
# Claude Code
cp commands/claude/eksekusi.md ~/.claude/commands/eksekusi.md

# OpenCode
cp commands/opencode/eksekusi.md ~/.config/opencode/commands/eksekusi.md
```

## Cara pakai

**1. CLI 1 — buat plan**

```
buat plan untuk fitur login
```

Skill `plan-write` otomatis aktif dan menyimpan:
`~/.plans/2026-11-20_fitur-login.md`

**2. CLI 2 (baru) — eksekusi plan**

```
/eksekusi ~/.plans/2026-11-20_fitur-login.md
```

Skill `plan-execute` membaca plan, mengerjakan tiap langkah berurutan, mencentang
`- [x]` di file-nya, lalu melaporkan ringkasan.

## Kodex / Gemini CLI

`SKILL.md` adalah standar lintas-agent (didukung Claude Code, OpenCode, Cursor,
dan ekosistem `skills.sh`). Untuk Codex CLI (format `AGENTS.md`) dan Gemini CLI
(extension tersendiri), konten skill-nya generik dan bisa ditempel/diadaptasi
manual — tidak ada auto-install.
