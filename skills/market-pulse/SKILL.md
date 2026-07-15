---
name: market-pulse
description: >
  This skill should be used when the user wants a market pulse, a landscape refresh, or a weekly
  scan of their target problem space. Triggers on "run market pulse", "what changed this week",
  "refresh the landscape", "any openings this week", or on a weekly schedule. It spawns the
  market-radar sub-agent to scan the user's watchlist (target companies and products, standards
  bodies and repos, key industry voices), diffs findings against the prior pulse and the user's
  landscape research, updates context/market-pulse.md, flags stale claims in the content backlog,
  and presents a ranked list of engagement openings. Read-heavy; writes only market-pulse.md and
  staleness flags. It never drafts or sends outreach — openings feed the user's own judgment.
metadata:
  version: "0.1.0"
---

# Market Pulse

The sensing layer of the engagement engine. Keeps the research corpus (the landscape report and
the pulse file) current so that posts, comments, and DMs stay grounded in a live picture rather
than a decaying one. The corpus is the asset; content is a derivative.

## Files

- `context/market-pulse.md` — watchlist, known state, linked files, pulse history. This skill owns
  it. All user-specific paths (landscape report, content backlog) live in its **Linked files**
  section; never hardcode them.
- The landscape report (path from Linked files) — read-only here; propose edits, never silently
  rewrite.
- The content backlog (path from Linked files) — read to check freshness; update staleness flags
  only.
- `context/engagement-log.md` — read to avoid suggesting openings in threads that are already live.

## Flow

1. **Load state.** Read market-pulse.md (watchlist + last pulse date + known state) and skim the
   engagement log. If market-pulse.md is missing, bootstrap it from the template and confirm the
   watchlist with the user before scanning.
2. **Spawn the radar.** Launch the `market-radar` agent with everything user-specific in the
   prompt: the watchlist, a one-paragraph thesis summary (from the candidate profile / positioning
   context), the last pulse date, and the known-state facts. The agent carries no user assumptions
   of its own. One agent, one pass. Do not scan inline in the main session.
3. **Receive and reconcile.** Take the radar's brief. Cross-check anything that contradicts the
   known state before accepting it (one verification fetch is fine here).
4. **Write the pulse.** Append a dated entry to market-pulse.md: what changed, staleness flags,
   openings, watchlist changes. Update the known-state section in place.
5. **Flag, don't fix.** For each staleness flag that touches the landscape report or a content
   draft, add an UPDATE REQUIRED note at the relevant spot (or list it in the pulse entry if the
   file is outside this skill's write scope). Never rewrite the user's prose.
6. **Present.** In chat: a five-minute read. What changed (dated, sourced), what's now stale, the
   top 3 openings with suggested angles, and one recommended action. No wall of text; the full
   detail lives in the file.

## Openings discipline

An opening is only worth presenting if the user's corpus gives him something no generic commenter
has: a claim his thesis refines, a question his shipped experience answers, or a thread his prior
exchanges earned him standing in. Rank by (relevance to active pipeline) x (freshness of thread).
Mark any opening involving a person already in the engagement log with their current thread state,
so the user never double-messages a pending thread.

## Cadence

Designed for weekly scheduled runs plus on-demand invocations before publishing anything from the
content backlog. When invoked by a schedule, still end with the chat summary; the user reads it
async.
