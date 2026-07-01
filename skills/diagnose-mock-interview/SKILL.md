---
name: diagnose-mock-interview
description: "Diagnose mock PM interview transcripts — peer mocks, self-practice recordings, or draft answers — using the Navigation vs Judgment framework, prescribe specific coaching fixes, and track whether the user is improving or stuck over time. Use this for practice sessions only, NOT for real interview rounds (those use interview-debrief). Trigger whenever the user shares a transcript or answer for feedback, asks how their mock interview skills are progressing, or wants coaching on a practice run."
---

# Interview Transcript Diagnostician

## Purpose

Diagnose what went wrong, name the specific behavior to change, and track whether the fix is landing — session over session. Not generic feedback. Not a long report. The one thing the user needs to do differently next time, and an honest read on whether they're improving.

---

# Step 0: Confirm Scope

Before diagnosing, confirm which lines are the user's candidate answers. If it can't be determined from the transcript and context, ask first. Do not guess.

Transcript types:
- **Solo answer or draft**: the user is the candidate. No ambiguity.
- **Peer mock, clearly labeled**: Obvious from speaker tags.
- **Ambiguous**: Ask. "Quick check before I dig in — were you the candidate, the interviewer, or both in this one?"
- **the user was the interviewer for someone else**: Do not diagnose as the user's performance. Do not log. Ask whether they want feedback on the candidate's answer for general learning value.

Once confirmed, diagnose only the user's candidate lines.

**Save transcript immediately:** After confirming scope (and only if the user is the candidate), write the raw transcript to `Recordings & Transcripts/Peer Mock Interviews/[YYYY-MM-DD]-[question-type].md`. Question type = short slug derived from the question (e.g., `pricing`, `product-sense`, `metrics`, `execution`). Do this silently before any analysis.

---

# Historical Progress Tracking

## Log file

The log lives at `context/mock-diagnostics-log.md`.

This is C4 — the same file the interview-prep-brief skill reads to surface coaching reminders. Writing here keeps mock-session insights available to future prep briefs automatically.

This folder must be connected to Cowork before diagnosing. If it isn't connected, ask: "Quick check — is your connected job-search folder connected? I need it to read and update your progress log."

If the file doesn't exist yet, create it with this header:

```markdown
# Mock Interview Diagnostics Log

*Written by: diagnose-mock-interview | Read by: diagnose-mock-interview, interview-prep-brief (as C4)*
*Append-only. Newest entries at the bottom.*
*Scope: case study / product mock questions only — NOT real interview rounds.*
```

## Before diagnosing: read the log

Check:
- Has this failure subtype appeared before, and how many times?
- Was a fix prescribed? Does this session show it landing?
- Is the user improving, flat, or stuck on this issue?

If the log is empty, this is the baseline session. Say so.

## After diagnosing: append an entry

```markdown
## [YYYY-MM-DD] - [Question type]

- Dominant failure: [subtype] - [severity]
- What happened: [one line, evidence-grounded]
- Fix prescribed: [one-line behavior change]
- Status: New / Improving / Stuck ([N] sessions)
```

---

# Core Diagnostic Model

Every failure is either **Navigation** or **Judgment**.

**Navigation** (process/routing): the user went to the wrong place — wrong objective stated, wrong frame, wrong sequence, wrong time allocation, missed the core decision. The fix is changing what you do first or what step you prioritize.

**Judgment** (reasoning/substance): the user was in the right place but the reasoning inside it was weak — unstated assumption, thin conclusion, missing tradeoff, failed to defend. The fix is changing what you say inside a step.

Classify before diagnosing. The distinction matters because the fixes are different.

---

## Navigation Failure Subtypes

For each: what it looks and feels like as it's happening, and the recovery move.

### No optimization objective
**What it looks like:** You're building a framework — segments, options, criteria — before stating what the framework is optimizing for. You have a process but no anchor.
**Early warning sign:** 60 seconds in, you're segmenting or listing options but haven't said "we're optimizing for X over Y."
**Recovery:** "Before I go further — I'm assuming we're optimizing for [X] over [Y], because [reason]. Flag it if that's wrong and I'll adjust."

### Missing center of gravity
**What it looks like:** You've named the topic area but not the specific decision or tension the question is actually testing. The interviewer isn't sure what problem you're solving.
**Early warning sign:** You could summarize what you've said so far as "here's some relevant context" rather than "here's the decision I'm working toward."
**Recovery:** "Let me name what this is really testing: the core tension is [X vs. Y]. That's what I'll structure my answer around."

### Wrong sequence
**What it looks like:** Right ingredients, wrong order. You're analyzing tradeoffs before stating the options, or making a recommendation before establishing what good looks like.
**Early warning sign:** You've reached a step that requires the output of a prior step you skipped.
**Recovery:** "Before I go deeper here, let me first [state the objective / lay out the options / name the tension] — that'll make this analysis more grounded."

### Wrong time allocation
**What it looks like:** Most of your time went to low-value setup or exploration; you ran out of time for the actual decision.
**Early warning sign:** You're 70% through your time and haven't committed to a recommendation.
**Recovery:** "I want to make sure I get to a recommendation — let me commit to [X] and use the remaining time to defend it."

### Delayed recommendation
**What it looks like:** You keep finding more to analyze instead of committing. The answer stays open-ended too long.
**Early warning sign:** You feel like you "need more information" before picking, or you're listing considerations without converging.
**Recovery:** "My current hypothesis is [X]. I'm going to commit to that and pressure-test it, rather than keep analyzing before I pick."

---

## Judgment Failure Subtypes

### Weak assumption
**What it looks like:** You're using a number, premise, or claim without stating it. It drives your reasoning but lives underground.
**Early warning sign:** You cite a figure or make a choice without a "because." The premise is implicit.
**Recovery:** "I'm going to flag that as an assumption: roughly [X], because [directional reason]. I'd want to validate it with [test or data]."

### Weak conclusion
**What it looks like:** Your recommendation doesn't clearly beat the alternatives you named, or doesn't follow from your own stated criteria.
**Early warning sign:** If you asked "why this recommendation over the next-best option" you'd struggle to answer cleanly.
**Recovery:** "Pressure-testing this against [alternative]: the reason I'd still choose this is [principle or specific evidence]."

### Weak tradeoff
**What it looks like:** You made a recommendation without naming what you're sacrificing or what risk you're accepting.
**Early warning sign:** Your recommendation sounds like a pure win — no downside, no sacrifice mentioned.
**Recovery:** "The tradeoff I'm accepting here is [X] over [Y]. The risk I'm taking on is [Z], and here's why it's worth it."

### Weak defensibility
**What it looks like:** Your answer is plausible but collapses under pushback. You retreat without defending from a principle.
**Early warning sign:** When challenged, you open with "that's a fair point" and then soften your position without a reason.
**Recovery:** "I'll defend this from first principles: [principle]. That's why I'd hold the recommendation even given [the counterargument]."

### Missing customer/business logic
**What it looks like:** The recommendation floats free — it doesn't connect to specific customer pain or a business outcome.
**Early warning sign:** Your answer describes what to build or do, but not why a customer would care or what it moves for the business.
**Recovery:** "Connecting this back: the customer pain is [X], which this solves by [Y], and the business value is [Z]."

---

## Severity

**Critical** — likely changes the outcome: no recommendation reached, missed the core decision, strategically wrong conclusion, wrong frame for the question type.
**Important** — materially improves quality: weak tradeoff, missing assumption, incomplete logic, doesn't survive pushback.
**Minor** — polish: phrasing, a sharper metric, an unnecessary tangent.

Flag Critical issues first. Do not weight all findings equally.

---

# Evidence Rule

For every Critical or Important failure, cite what actually happened in the transcript: what the user said, what the interviewer pushed on, what that indicates. Diagnose from this session's evidence, not from pattern alone.

If the progress log shows a recurring issue but this session doesn't show it, say so explicitly — that's useful signal too.

If a coach's or partner's feedback is in the transcript: treat their questions and pushback as evidence (they show where the answer was tested). Treat their verdicts and suggested fixes as opinions — run them through this framework independently. If the coach's read diverges from this diagnosis, say so in one line and note which read the evidence better supports.

---

# Required Output Format

**Four sections.**

---

## Section 1: Overall Verdict

Three lines:
1. **Question type:** [category] — [specific prompt in one phrase, e.g., "Pricing — 10x-capable / 10x-cost AI model"]
2. **Question:** [The actual question as asked, verbatim or close paraphrase — enough that this section is self-contained without the transcript]
3. Interview-bar verdict + one sentence on what drove it — what specifically cost the user the higher rating.

Then one more line:
4. One sentence on what a Hire answer would have done differently — concrete and specific to this session, not generic.

Verdicts: Strong hire / Hire / Lean hire / Borderline / Lean no / No hire

Example:
"**Question type:** Pricing — 10x-capable / 10x-cost AI model
**Question:** You're a PM at Google. We have a new AI model that's 10x more capable but costs 10x more to run. How would you price it?
Lean hire. The answer required too much interviewer steering before arriving at the right framing.
A Hire answer would have stated the optimization objective (market share over margin) in the first 60 seconds, making the segmentation feel purposeful rather than redirected."

---

## Section 2: Diagnosis

Start with one sentence on what worked — a specific behavior or moment the user did well that should be preserved. Even when the answer had significant failures, name at least one thing done right.

**What worked:** [One sentence. Name a specific behavior or moment that was strong, grounded in the transcript.]

Then diagnose failures (maximum two). For each, use this format:

- **Dominant failure:** [Navigation / Judgment] — [subtype]
- **Severity:** Critical / Important / Minor
- **What happened:** [One sentence. Cite the specific moment.]
- **Downstream impact:** [What this failure cost in the answer — what went wrong as a direct result.]
- **Leverage:** High / Medium / Low — [One sentence on what fixing this would unlock.]
- **Fix:** [One sentence. Name the replacement behavior.]
- **Say this:** "[Exact sentence to use next time.]"

If there's a second failure worth naming, add it in the same format after the first. Maximum two failures per session. Do not list more — prioritize the highest-ROI issue.

---

## Section 3: Coach Check-In

This is the most important section. Assess the user's trend on the failure(s) just diagnosed, using the progress log.

**If this failure is new:**
Name it as new. One sentence on what to watch for next session.

**If the user is improving** (same failure appeared before but is less severe, or a prescribed fix is visibly landing):
Name exactly what changed — cite the specific moment in this session that shows the improvement. One sentence on what to work on next. Tone: genuine acknowledgment, not hollow praise.

**If the user is stuck** (same Critical or Important failure has appeared 3+ sessions with no sign of the fix landing):

First, assess whether you can infer the blocker from the session evidence.

If confident: offer a hypothesis. "We've hit [X] for [N] sessions. My read on what's making this hard to change is [specific hypothesis based on what you observed]. Does that match what you're experiencing?"

If unsure: ask a targeted clarifying question. "We've hit [X] for [N] sessions and the fix doesn't seem to be landing. I want to understand what's getting in the way — [specific question about what makes it difficult in the moment]."

Do not just restate the failure and repeat the same prescription. If it hasn't landed after three sessions, the prescription or the framing needs to change.

**When failures have mixed status** (e.g., Failure 1 is improving, Failure 2 is new): Lead with the higher-severity or longer-standing issue. Acknowledge both, but be explicit about the priority — "The more urgent thing to keep working on is X; Y is new and we'll see if it recurs."

**Tone throughout:** Direct, warm, honest. Like a coach who has been watching closely and cares whether the fix actually lands — not a grading system producing scores.

---

## Section 4: Full Answer Scaffold

Always include this section. Pull the relevant question-type scaffold from `references/thinking-scaffolds.md`. Produce a 4-column table:

| Step | Question to ask yourself | the user's performance | Tips |

The Step column includes the approximate time target from the scaffold. The first row is always the clarifying questions step:

| 0. Clarifying questions (~1-2 min) | What do I need to understand before starting — and what can I state as an assumption instead of asking? | [the user's performance on clarifying questions — what they asked, what they missed, what they should have stated as an assumption] | [The specific questions to ask for this question type; what to assume vs. ask; how long to spend] |

Then continue with the numbered scaffold steps. Show every step in the scaffold — including steps the user did well.

For "the user's performance", evaluate every step using:
- ✅ Did this — brief note if useful, or leave blank if clean
- ⚠️ Partial — what happened, what was missing or needed prompting
- ❌ Didn't do this — brief note on what was absent

Show every step in the scaffold — including steps the user did well. The full picture of what worked and what didn't is part of the value. Do not show only the failure steps.

---

# Guardrails Against Overfitting

- Treat patterns from the progress log as hypotheses, not ground truth. Verify every diagnosis against this session's evidence.
- Don't assume Navigation is dominant because it has been before. Check both categories.
- The question-type scaffolds in the reference file are strong defaults, not rules. Pressure-test them against the actual prompt.
- A coach's or partner's verdict isn't ground truth. Diagnose independently.
- If the routing table's structure doesn't fit the prompt, say so rather than forcing the fit.

---

# Final Rule

Never stop at diagnosis. For every failure named, provide:

1. Failure type and subtype
2. Severity
3. What happened (evidence from this session)
4. Replacement behavior
5. Exact sentence to say next time

If the user was confirmed as the candidate: read the progress log, write the coach check-in, append the new entry to `context/mock-diagnostics-log.md`.

The goal is not a thorough review. The goal is one behavior that changes, visible in the next session.
