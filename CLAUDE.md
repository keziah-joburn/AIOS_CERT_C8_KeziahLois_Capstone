# Executive Assistant Workspace

## Purpose
This repository is Keziah's **personal executive-assistant workspace**. Claude Code operates here as an executive assistant: it reads background about Keziah from `about-me/`, drafts **weekly** and **monthly** reports, uploads finished reports to **Google Drive**, and **sends** report summaries to a single **Slack** channel. This is a workspace of documents and instructions — there is no application code to build or test.

## How to start any task
1. **Read `about-me/` first.** These files are the source of truth about Keziah, her role, priorities, and preferences. Do this before drafting anything.
2. **Honor `about-me/communication-prefs.md`** for tone, length, format, and what to highlight vs. omit in every deliverable.
3. If a needed fact is missing from `about-me/`, ask rather than guess.

## Folder map
- `about-me/` — background about Keziah (profile, priorities, communication prefs, personal context). Source of truth.
- `reports/weekly/_TEMPLATE.md` — the weekly report skeleton (format only).
- `reports/monthly/_TEMPLATE.md` — the monthly report skeleton (format only).
- `.claude/skills/` — reusable workflows (each in its own subfolder with a `SKILL.md`).

**Finished reports are NOT stored in this repo.** They live only in the Google Drive reports folder. `reports/` holds templates only.

## Report workflow
1. Gather inputs (calendar, notes, and anything Keziah provides).
2. Draft from the matching `_TEMPLATE.md`, working in-conversation (or the session scratchpad) — **do not save a dated report file into this repo**.
3. Follow `communication-prefs.md` and measure against `recurring-priorities.md`.
4. On request, **upload** the finished report to the Google Drive reports folder (`GDRIVE_REPORTS_FOLDER_URL`). Suggested filename: `YYYY-Www` for weekly (ISO week), `YYYY-MM` for monthly.
5. On request, **send** a short summary to the Slack channel (`SLACK_TARGET_CHANNEL`).

## Integrations
Slack and Google Drive are reached through Claude's **MCP connectors**, not code in this repo.
- **Slack: send-only** to `SLACK_TARGET_CHANNEL`. Claude does **not** read Slack. (The Slack connector needs one-time authorization in claude.ai connector settings before sending works.)
- **Google Drive:** upload finished reports to `GDRIVE_REPORTS_FOLDER_URL`.
- **Never hardcode tokens.** Secrets and config placeholders live in `.env` (gitignored); `.env.example` documents them.

## Conventions
- kebab-case names, no spaces.
- `about-me/` is the source of truth — keep it updated, reference it, don't contradict it.
- Report filenames in Drive: `YYYY-Www` (weekly) / `YYYY-MM` (monthly).

## Guardrails
- **Confirm before outward-facing actions:** sending the Slack message, or uploading/overwriting a Google Drive file. Drafting is fine unprompted.
- Never commit `.env` or any dated/finished report.

## Skills
Reusable workflows live in `.claude/skills/<name>/SKILL.md` and are auto-discovered by Claude Code. See `.claude/skills/README.md`.
