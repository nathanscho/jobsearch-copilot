---
name: engagement-sync
description: >
  This skill should be used when the user wants to sync their networking/engagement state.
  Triggers on "sync engagement", "engagement status", "whose turn is it", "update the engagement
  log", "who should I engage next", or as a step inside the daily digest. It reconciles the
  engagement log against reality — the LinkedIn inbox connector (e.g., Kondo) for DM thread
  states, plus any inbound signals the user supplies (profile-viewer or post-analytics exports) —
  then runs a targeting pass that scores new engagement opportunities and refreshes the action
  queue. Read-only toward the outside world: it never sends messages, connection requests, or
  reactions, and never surfaces connector-internal identifiers. Writes only context files.
metadata:
  version: "0.1.0"
---

# Engagement Sync

The reconciliation and targeting layer of the engagement engine. The inbox connector is the source
of truth for DM state; `context/engagement-log.md` is the working-notes layer on top (thread
context, next moves, house rules). This skill keeps the two honest with each other, then tells the
user where their attention is owed and where it would pay best. It is to engagement what
`jobsearch-status` is to the pipeline.

## Files and sources

- `context/engagement-log.md` — this skill owns its **State**, **History**, and **Action queue**
  maintenance. Human owns the decisions recorded in it.
- LinkedIn inbox connector (e.g., Kondo), if configured — chats, connections, invitations.
  Only recently-opened chats may have stored messages; fetch a chat's history before concluding
  anything about it. If no connector is configured, run in log-only mode and say so.
- `context/market-pulse.md` — openings and staleness flags from the latest pulse.
- `context/pipeline-state.md` and `context/target-company-map.md` — relevance scoring inputs.
- Inbound signals (optional, user-supplied): post analytics exports, profile-viewer lists.
  These cannot be fetched automatically; if the user hasn't supplied fresh ones, note it, never
  fabricate inbound data.

## Flow

1. **Reconcile.** For each active thread in the log with a DM channel: check the connector for
   the real state. Classify: `my-turn` (they replied last), `awaiting` (user's message is the
   latest), `quiet` (awaiting AND past the thread's follow-up date), `closed`. Update the log's
   State lines with dates. Never mark a thread replied without connector evidence; when the
   connector lacks message history for a thread, fetch it, and if still unknown, mark
   `unverified` rather than guessing.
2. **Catch strays.** Surface connector threads and accepted invitations that are NOT in the log
   but plausibly belong (contacts at watchlist or pipeline companies). Propose additions; do not
   silently create entries.
3. **Targeting pass.** Merge candidate opportunities from: market-pulse openings, inbound signals
   (if supplied), new connections/invitations, and network adjacency to active loops. Score each:
   **pipeline relevance × standing (existing warmth) × freshness (thread/post age) × unique angle
   (does the user's corpus give them something non-generic to say)**. Respect thread states —
   never propose engaging someone whose thread is `awaiting`. For every candidate, before it can
   be presented, write down what would concretely happen for the user's pipeline if this landed
   well (an interview, a warm intro, a role tip, visibility with a specific hiring team) — a
   score with no consequence attached is not a finished evaluation.
4. **Refresh the queue.** Mark done items done (with evidence), roll quiet threads into dated
   follow-up items, append top-scored targets as new items tagged `(proposed)`. The user confirms
   proposals by keeping them; the skill never deletes a human-authored queue item.
5. **Present.** A short brief: (a) Your turn — threads awaiting the user's reply; (b) Quiet —
   threads past follow-up date with a suggested next move each; (c) Queue changes; (d) Top 3
   proposed targets. End with the single highest-leverage action of the day. **Every item in every
   section — queue, quiet-thread nudges, and proposed targets alike — must state its concrete
   payoff and its cost of ignoring it, not just a label or a score.** The test: could the user
   decide to act (or not) from this line alone, without asking "why does this matter"? If not,
   rewrite it. Generic justifications ("good networking opportunity," "worth engaging") are a
   failure of this step, not a style choice.

   **Format, not just content:** the payoff and the cost-of-waiting are two different pieces of
   information and must not be fused into one paragraph — the cost of waiting is what tells the
   user how urgent this is, so it needs to be scannable on its own, not buried mid-sentence.
   Structure each item as:
   - A one-line action/headline.
   - A sub-bullet stating the payoff (why this matters, in mechanism terms).
   - A second sub-bullet stating the cost of waiting, opening with an urgency tag that pairs a
     fixed emoji with its plain-word meaning (always both together, so the emoji is never asked
     to carry meaning alone): ⏰ **TIME-SENSITIVE** for a real external closing window,
     ⚠️ **RELATIONSHIP RISK** for possible damage to the thread if acted on wrong,
     🟢 **LOW URGENCY** for safe to defer, nothing decays, ✋ **HOLD** for items where the correct
     action is deliberately waiting. Print this exact four-item legend once at the top of every
     brief, above the first section. Use exactly one tag per item, chosen for actual urgency, not
     applied uniformly.
   This is a rendering requirement, not a suggestion — a brief where urgency is inline prose
   instead of a tagged sub-bullet, or where the legend is missing, has not satisfied this step.

## Guardrails

- Read-only externally. Drafting belongs to the user (with the fact-checker as exit gate);
  sending belongs to the user alone.
- One-ask discipline: when suggesting a next move on a quiet thread, it is always one light
  nudge with a new angle, never a repeat of the unanswered ask.
- Respect the log's house rules section in every suggestion.
- Refer to people by name only; never expose connector-internal IDs (per connector guidance).
- If both the connector and the log are silent on a question, say "unknown" — this skill's value
  is that its picture is real.
