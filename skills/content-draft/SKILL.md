---
name: content-draft
description: >
  This skill should be used when the user wants to draft a LinkedIn post or a comment/reply on
  someone else's post or thread. Triggers on "draft a comment on [person]'s post", "write a
  LinkedIn post about X", "reply to [person]'s comment", "help me respond to this thread", or when
  the user pastes/screenshots a post or comment thread and asks what to say. Grounds every draft in
  the user's actual scope boundaries (candidate profile), thread state and house style
  (engagement-log.md), and current facts (market-pulse.md), then gates the draft through the
  fact-checker agent before presenting it as ready to ship. Never posts or sends anything itself —
  drafting and verification only.
metadata:
  version: "0.1.0"
---

# Content Draft

The drafting layer of the engagement engine. `market-pulse` keeps the facts current,
`engagement-sync` tracks who's owed what, `fact-checker` verifies before anything ships. This
skill is the piece that sits between them and the user: it takes a drafting request, pulls the
right context automatically instead of relying on the conversation to remember it, and never lets
a draft leave the building without passing the gate. If this skill isn't used, drafting still
happens conversationally with the same inputs and the same gate — this just makes sure none of it
gets skipped.

## Files

- `context/candidate-profile.md` (C2) — scope boundaries (what the user built vs. contributed to
  vs. GTM'd) and positioning thesis. Read-only.
- `context/engagement-log.md` — thread state (never draft into a thread that's `awaiting` the
  other party without explicit user override) and the Rules of engagement house style section.
  Read-only here; the user or `engagement-sync` updates it after something ships.
- `context/market-pulse.md` — known-state facts and staleness flags. Read-only. If a fact the
  draft leans on is flagged stale, surface it before drafting, don't draft around it silently.
- Content backlog (path from market-pulse.md's Linked files section), if drafting a new post from
  an existing idea rather than a fresh one. Read-only; propose edits, never silently rewrite.
- `fact-checker` agent — spawned in Step 3, not read directly.

## Flow

1. **Identify the draft type and source material.**
   - **New post:** pull from the content backlog if the user references a draft idea, or work from
     what the user describes fresh. Check market-pulse.md's staleness flags against anything the
     post will assert as current.
   - **Comment or reply:** the source is the post/thread itself — a paste, screenshot, or the
     user's description. Read it in full before drafting; a reply to a claim you haven't actually
     read is how threads go sideways. Check `engagement-log.md` for this person's thread state
     first. If `awaiting` (their turn hasn't come, or the user already has an unanswered ask out
     to them), stop and flag it rather than drafting a second ask on top of an unanswered one.

2. **Load context.** Pull scope boundaries from candidate-profile.md (what's fair to claim as
   first-person experience) and the house style rules from engagement-log.md (banned punctuation,
   register, scope-discipline line). Both apply to every draft regardless of type.

3. **Draft.** Write to the house style rules. In addition, apply these craft defaults unless the
   user's house style says otherwise:
   - Open like a peer reacting to something specific, not a critic issuing a verdict. Avoid
     opening lines that grade or pronounce judgment on the post itself ("this is the proof point
     that...", "this is exactly right") — react to a specific detail instead.
   - Don't name-check the other person's biography or work history (former employer, past role,
     old product) unless it's already live in the thread or the user has an established
     relationship with them. An unearned biographical callback in a first comment reads as "I
     looked you up," which is a tell, not a connector. Let technical or substantive points stand
     on their own; the research can inform the question without appearing in the sentence.
   - Concede real points plainly before pushing back; don't bury agreement inside a rebuttal.
   - One real question or one real point of pushback per draft, not several stacked together.
   - No claim in the draft should exceed what candidate-profile.md's scope boundaries support.
     If the draft would be stronger with a claim the user can't actually back, flag the gap rather
     than writing around it vaguely.

4. **Check platform constraints.** If a character limit applies (e.g., a LinkedIn comment), never
   guess the limit or eyeball the length — get an exact character count (a quick script/count
   check, not a visual estimate) and compare against the limit the user states or the platform's
   known cap. If over, trim by cutting or tightening content that isn't load-bearing to the core
   point(s); state which points were preserved and re-count to confirm the trim actually worked.

5. **Fact-check gate.** Spawn the `fact-checker` agent with: the draft, the scope-boundary excerpt
   from candidate-profile.md, and the house style rules from engagement-log.md. This step is not
   optional and does not wait for the user to ask for it — house rule 5 in engagement-log.md
   already commits to it. Do not present a draft as ready to ship before this returns.

6. **Present.** Show the draft, the fact-checker's verdict (SHIP / FIX FIRST / DO NOT SHIP) and any
   flagged claims, and, if trimmed, the before/after character count. If the verdict is FIX FIRST
   or DO NOT SHIP, lead with that, not with the draft, and explain the specific fix needed before
   showing revised text. Remind the user (briefly, once) that posting is theirs to do, and that
   `engagement-sync` should pick up the new thread state next time it runs.

## Guardrails

- Never post, send, or reply on the user's behalf. This skill produces text; the user ships it.
- Never treat "I already read the thread earlier in conversation" as sufficient if new screenshots
  or pastes have been shared since — re-read what's actually in front of you before drafting into
  it.
- If engagement-log.md, market-pulse.md, or candidate-profile.md are missing, say so and fall back
  to whatever the user supplies directly in the conversation; don't block entirely on missing
  infrastructure.
- Style rules in engagement-log.md always win over this skill's defaults if they conflict.
