---
name: positioning-thesis
description: >
  This skill should be used when a user wants to work out how to position themselves in the job market —
  which roles to target and how to frame their background. Triggers on "help me with positioning", "what
  should I target", "what roles fit me", "position myself", "figure out my angle", or during setup after
  the resume is loaded. The user shares their resume plus a few target job links; the skill analyzes the
  real demand across those JDs, maps the user's background against it, and proposes 2-3 credible
  positioning profiles — each with a thesis, the experience and stories to foreground, real
  differentiators, likely objections, and trade-offs. It also exposes blindspots: adjacent role profiles
  the user is clearly qualified for but hasn't considered, each grounded in evidence from their
  background. Writes the candidate profile (C2) only after the user confirms. Never inflates fit or
  invents qualifications.
metadata:
  version: "1.1.0"
---

# Positioning Thesis

Help the user decide *who to be* in the market — what roles to target and how to frame themselves —
derived empirically from real target job descriptions, not from generic advice. This produces or sharpens
the candidate profile (C2), the file everything else depends on.

## Grounding rules (read first)

- **Evidence only.** Every claim about the user's fit must trace to something real in their resume or
  context files. Never inflate fit, invent qualifications, or assert a strength the evidence doesn't
  support. If fit for a role is weak, say so plainly.
- **Analyze real JDs.** Work from the actual job descriptions the user shares. If a link won't load, ask
  them to paste the text — do not guess what the role wants.

## Inputs

- The user's resume and candidate profile (C2 draft, if setup already bootstrapped one).
- 3-6 target job links or pasted JDs. If the user gives fewer, proceed but note the signal is thinner.
- Search constraints (C7) if they exist — level, comp, location — to keep proposals realistic.

## Workflow

### Step 1 — Gather

Confirm you have the resume, and ask the user for a few (ideally 3-6) job links that represent what
they're drawn to. Fetch and read each JD.

### Step 2 — Analyze the demand

For each JD, extract what the role is *really* hiring to solve (not the boilerplate): the core problem,
the must-have competencies, the level, the domain. Then cluster across them: what's common to all, and
what distinct archetypes exist (e.g., "platform/infra PM" vs "0-to-1 applied-AI PM" vs "governance PM").

### Step 3 — Map the user against the demand

From the resume and context, map the user's real evidence — experience, shipped work, skills, metrics —
onto each cluster. Be honest about where they're a strong, credible fit and where there are genuine gaps.

### Step 4 — Blindspot pass (do this deliberately)

Independent of the links they shared, look at the user's demonstrated skill set and ask: **what other
role profiles is this person clearly qualified for that they did NOT include?** People often confine
their search to one lane and miss an adjacent one their background fits well. Surface 1-2 such
blindspots — but only where the evidence genuinely supports it — and name the specific experience that
qualifies them (e.g., "you only shared platform-PM roles, but your governance and trust work makes you a
strong fit for [X], which none of your links cover"). If the evidence doesn't support a real blindspot,
don't manufacture one.

### Step 5 — Propose 2-3 target job profiles

Present 2-3 credible **target job profiles** the user could target — these map directly onto the
"Target job profiles" section of `candidate-profile.md` (C2), so name and frame them as the confident,
active positioning case for each, not a passive analysis. Include at least one blindspot-derived option
if the evidence supports it. For each profile:
- **Name** (the role/domain class) and a one-line **pitch** ("who you are for this kind of role" —
  confident and specific, not a skills list).
- **Proof points:** which experience and which stories (from C1) to lead with, drawn from real evidence.
- **Differentiation:** the real, evidenced edges — what makes this candidate's version of the pitch
  different from a typical candidate targeting the same profile.
- **Watch-out:** what this positioning invites an interviewer to probe, and the honest answer.
- **Target companies:** if the conversation surfaces specific companies that fit this profile, note them
  here for Step 7 to carry into C3 — don't force this if nothing concrete comes up.
- **Trade-off:** e.g., strongest-fit but narrower market vs. wider market but more competition vs. comp
  ceiling. Help them see what each choice costs and opens.

### Step 6 — Discuss and choose

Ask which profiles resonate, which they'd rule out and why. Their reactions are real signal — capture
them. The user may pick one primary positioning, a primary + secondary, or ask to refine.

### Step 7 — Write C2 (gated)

With the user's confirmation, update `candidate-profile.md` (C2) using its active-voice structure: the
positioning statement, 2-3 **target job profiles** (each with its pitch, proof points, differentiation,
watch-out, and target companies), the search thesis, and known gaps with honest responses. If C2 already
has job profiles from `setup-jobsearch`, **reconcile rather than overwrite** — sharpen or replace a
profile that's clearly superseded, but don't silently drop a profile the user hasn't ruled out. **Never
write C2 without explicit confirmation.** Reflect their real words and choices, not an idealized version.

If any profile picked up specific target companies during the conversation, also propose adding them to
`target-company-map.md` (C3) under that profile's section — same confirmation gate. Keep C2 and C3 in
sync: every profile named in one should be represented in the other.

## Hand-offs

- Build the stories that support the chosen positioning → `story-bank-builder`
- Tactical prep for a specific round → `interview-prep-brief`
- How positioning has *performed* across rounds (backward-looking) → `jobsearch-coach` (deep-review mode)
