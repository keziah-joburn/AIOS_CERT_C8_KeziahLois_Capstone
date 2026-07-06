---
name: weekly-report
description: Creates Keziah's weekly report — asks about her week, drafts a 4-part report (summary table, productivity analysis, next-week focus, Slack summary), uploads it to the Drive reports folder, and sends the summary to Slack. Use when Keziah asks for a weekly report or a weekly update/summary.
---

# Weekly Report

Copy this checklist and track progress:

```
Weekly Report Progress:
- [ ] Step 0: Read about-me/ files
- [ ] Step 1: Ask about the week
- [ ] Step 2: Draft the report
- [ ] Step 3: Upload to Google Drive
- [ ] Step 4: Confirm and send Slack summary
- [ ] Step 5: Report outcomes
```

## Step 0: Read about-me/ first

Read `about-me/professional-profile.md`, `about-me/recurring-priorities.md`, and `about-me/communication-prefs.md` before drafting anything. Follow `communication-prefs.md` for tone/length/format and measure the week against `recurring-priorities.md`.

**Red line:** never invent numbers. If a metric wasn't reported, say "not tracked" rather than guessing.

**Writing style** (applies to both the report and the Slack message):
- No em dashes. Use a period, comma, or parentheses instead.
- No AI-sounding stock phrases or transitions: "it's important to note," "in today's fast-paced," "dive into," "unlock," "seamless," "leverage," "robust," "furthermore," "moreover," "overall," "in conclusion."
- Write like Keziah would actually type it: short, direct, first person. Match `communication-prefs.md`.

## Step 1: Ask about the week

Ask Keziah (use AskUserQuestion where useful):
- What did you get done this week?
- How many hours did you work this week?
- Any blockers you faced this week?
- Are there any pending tasks not accomplished this week?
- What are your plans next week?

If an answer is high-level or ambiguous in a way that would change how the report reads (e.g. it implies zero activity in a tracked priority area), confirm with Keziah before writing it into the report as fact.

## Step 2: Draft the report

Draft in-conversation or in the scratchpad — do **not** save a dated report file into this repo (`reports/` holds templates only).

**Document title:** `Keziah Mendoza - Weekly Report - MM/DD/YYYY` (use the date Keziah is preparing the report for).

Use this exact 4-part structure:

1. **Summary table** — tasks finished, hours worked this week, pending tasks.
2. **Productivity & focus analysis** — 5–7 sentence first-person paragraph on how productive the week was and where focus went, measured against `recurring-priorities.md`.
3. **Next week's focus** — bullet list of what Keziah aims to get done.
4. **Slack summary** — one paragraph: a summary of the week's performance + one sentence on next week's aim.

## Step 3: Upload to Google Drive

Read `GDRIVE_REPORTS_FOLDER_URL` from `.env` and extract the folder ID from it.

Use `mcp__claude_ai_Google_Drive__create_file` (load its schema via ToolSearch if not already loaded) to create a Google Doc:
- `title`: the document title from Step 2
- `parentId`: the Drive folder ID
- `textContent`: the full report, `contentMimeType: text/markdown`

Capture the returned `viewUrl` — this is the report link used in Step 4.

## Step 4: Confirm, then send the Slack summary

This is an outward-facing action — confirm the exact message with Keziah before sending (per CLAUDE.md guardrails).

Read `SLACK_TARGET_CHANNEL` from `.env`.

Message format:
```
Hey @Mike, here's the summary of my weekly report:

[Slack summary paragraph from Step 2, part 4]

Full breakdown here: [Drive document link from Step 3]
```

Once Keziah confirms, send it with `mcp__claude_ai_Slack__slack_send_message` (load its schema via ToolSearch if not already loaded) to the channel from `.env`.

## Step 5: Report outcomes

Tell Keziah what happened: the Drive document link and the Slack message link. If either action failed, say so plainly rather than claiming success.
