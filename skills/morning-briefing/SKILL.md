---
name: morning-briefing
description: >-
  Build a ~10-line morning brief from calendar, unread mail, chat mentions, and
  open tasks, each line sourced. Use at the start of the day or when the user
  asks "what's open." Draft-only; fail a source instead of using stale data.
  Never send mail or change calendar events without approval.
---

# Morning briefing

One short brief for the start of the day. Sources cited. Missing sources called out, not faked.

## When to use

- User starts the day with "morning brief", "what's open", or "/gm"-style standup
- User wants calendar + inbox + chat + tasks collapsed into one screen
- After overnight messages piled up and they need a triage snapshot

## Required inputs and access

**Inputs**
- Time window (default: since last brief or last 12–16 hours)
- Optional focus: which calendars, inboxes, or chat workspaces matter

**Access (use only what is connected)**
- Calendar connector or calendar the Bot can read
- Email connector for unread / flagged
- Slack or other chat connector for mentions/DMs if available
- Tasks source if the user has one (Notion, Linear, etc.)

If a source is not connected, omit it and say so. Do not reuse yesterday's numbers or invent meetings.

## Steps

1. Pull each available source for the window. Note failures per source.
2. Rank what needs the user today: meetings soon, urgent mail, direct asks in chat, overdue tasks.
3. Write ~10 tight lines. Each line names the source (Calendar / Email / Slack / Tasks).
4. Separate "Needs you" from "FYI".
5. Draft zero outbound messages unless the user asked for drafts; even then, drafts only.
6. Stop. Do not send email, post in Slack, accept meetings, or close tasks.

## How to validate

- Every line traces to a real item from a source pulled this run
- Failed sources are listed under "Couldn't reach"
- No stale "as of yesterday" filler presented as current
- Nothing was sent or changed on the user's behalf

## Always ask for approval when

- Sending email or chat messages
- Creating, moving, or declining calendar events
- Marking tasks done or reassigning work
- Archiving or deleting inbox items

## Expected output

**Morning brief (≈10 lines)**
- Needs you: …
- FYI: …
- Couldn't reach: …
- Window: …
