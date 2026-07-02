---
name: story-bank-builder
description: >
  This skill should be used when a user wants to build out or strengthen their interview story bank.
  Triggers on "build my story bank", "help me with my stories", "do I have enough stories", "find gaps in
  my stories", "strengthen my stories", or during setup after the profile is drafted. Reads the user's
  stories (C1) and positioning (C2), maps coverage against the question types their target roles will hit,
  and flags gaps and weak spots. It then interviews the user to extract missing stories, structures each
  into the Hook-Stakes-Tension-Judgment-Impact-Lesson arc with routing tags, and pressure-tests them for
  follow-up probing. Strictly conservative: it never fabricates detail to make a story sound better — it
  identifies what is missing and prompts the user to supply the real thing, marking gaps rather than
  filling them. Writes C1 only after the user confirms. Also handles quick, ad-hoc additions of a single
  story, not just full build sessions.
metadata:
  version: "1.0.0"
---

# Story Bank Builder

Proactively build and strengthen the user's story bank (C1): find the coverage gaps, extract real stories
to fill them, and shape each into the story arc — without ever inventing anything.

## The one rule that governs everything

**Never fabricate.** Do not invent tension, stakes, resistance, numbers, results, or any detail to make a
story stronger. Your job is to *extract* the truth from the user and *structure* it — not to embellish
it. When a story is missing an element that would make it more powerful (a real metric, a sharper
conflict, a named stakeholder), **name the gap and ask the user for the real detail.** If they don't have
it, leave it marked as a prompt (e.g., *[add the real number if you have it]*) — never fill it with a
guess. A weaker true story beats a stronger invented one, because invented detail collapses the moment an
interviewer probes it. This is the whole point of the skill.

## Read + write

Read C1 (story-bank.md) and C2 (candidate-profile.md, for positioning and target roles). Write C1 only
with explicit confirmation (C1 writes are gated).

## Workflow

### Step 1 — Load and map coverage

Read the current stories (C1) and the user's positioning/target roles (C2). Build a coverage map: list
the question types the user's target roles will actually hit — behavioral (leadership, conflict, failure,
ambiguity, influence-without-authority, prioritization) and role-specific (technical-depth, product-sense,
0-to-1, metrics, whatever their positioning demands). Map existing stories onto those types.

### Step 2 — Flag gaps and weak spots

Show the user two things:
- **Gaps:** question types with no strong story ("you have nothing for a genuine failure/what-you'd-do-differently question").
- **Weak spots:** existing stories that are thin, lack a clear result, or wouldn't hold up under probing.

Present these as a ranked short list (2-3 most worth fixing first, given their target roles) and let the
user choose where to start. Do not decide for them.

### Step 3 — Extract a real story (interview, don't invent)

For the chosen gap, interview the user like a thoughtful coach drawing out *their* experience. Ask
targeted questions to surface each element:
- What was the situation and what was genuinely at stake?
- What made it hard — the real tension, the resistance, the fork?
- What did you actually do, and why did it take insight or nerve?
- What was the result? Is there a real number?
- What did it teach you?

Ask follow-ups where an answer is vague. If the user can't remember or doesn't have a detail (especially a
metric), that's fine — mark it as a prompt, never fabricate it.

### Step 4 — Structure into the arc

Shape the extracted material into the story format (see story-bank.md header): **Hook → Stakes → Tension →
Judgment → Impact → Lesson**, plus routing tags. Use only what the user gave you. Where a power-element is
still missing, insert a clearly marked bracketed prompt rather than inventing it. Show the drafted story
back and let the user correct it.

### Step 5 — Strengthen existing weak stories the same way

For thin existing stories, apply the identical posture: name what's missing that would strengthen it, ask
the user for the real detail, and only reshape with what they provide. Never embellish to "improve" it.

### Step 6 — Write C1 (gated)

With confirmation, write the new and updated stories into story-bank.md in the standard format, and update
the Quick Reference table so the prep-brief skill can route them. Never write without confirmation.

## Hand-offs

- Company or interviewer intel from an informal chat → `interview-debrief` / `interview-prep-brief` (this skill owns story intake, including quick one-off additions)
- Deciding which stories to foreground for which roles → `positioning-thesis`
- Using the stories for a specific round → `interview-prep-brief`
