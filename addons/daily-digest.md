# Optional add-on — Daily chat digest

This add-on is **optional** and requires a `~~chat` connector (Slack, Teams). Skip it entirely if you
run the co-pilot without chat.

## What it does

A scheduled morning task that runs `job-discovery` and `jobsearch-status`, then posts a digest plus
per-role cards to your configured chat channel. You react to the cards (👍 / 🤔 / ❌) and reply in the
thread with pipeline updates; the next `jobsearch-status` run reads those reactions and replies back
into your pipeline state.

**Engagement section (optional, requires `context/engagement-log.md`):** if the engagement log
exists, the digest also includes: today's action queue items (sends due, replies owed), threads gone
quiet past their follow-up date, any open staleness flags from `context/market-pulse.md`, and — if a
LinkedIn inbox connector (e.g., Kondo) is configured — a reconciliation pass: chats where the other
party replied since the last digest are surfaced as "your turn," and the engagement log's thread
states are updated to match reality before the digest renders. DM state comes from the inbox
connector; the log is the working notes layered on top, never a second source of truth.

The skills themselves never post to chat on their own — posting is orchestration, which is why it lives
in a scheduled task rather than inside a skill. This keeps the skills side-effect-free and safe to run
on demand.

## Setup

1. Confirm a `chat_connector` and `chat_channel_id` are set in `context/config.md`.
2. Create a scheduled task (ask Claude: "set up my daily job search digest every weekday at 8am").
   The task prompt should: run job-discovery on the latest digest, run jobsearch-status, then post the
   digest + role cards to the chat channel from config.
3. Each morning, triage the cards with reactions and thread replies. The pipeline stays current
   automatically.

## Why it's separate from the core skills

- The core skills are read-and-write-files only. They are safe to invoke any time with no outbound side
  effects.
- Posting, scheduling, and reaction-reading are orchestration concerns handled here, so users without a
  chat connector get the full system with zero chat dependency.
