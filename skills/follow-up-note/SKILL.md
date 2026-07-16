---
name: follow-up-note
description: >
  Generate a strategic follow-up note after an interview, mentoring session, or networking call. Leads with an appropriateness verdict (Not Appropriate / Borderline / Send It), explains what sending would accomplish and how the recipient will likely perceive it, then generates personalized drafts anchored to specific moments — not generic topics. Interview mode supports 2-3 drafts per notable moment and an optional 30/60/90 plan for final-round decision-maker conversations. Mentoring and networking modes generate a structured note with a specific call to action.
metadata:
  workflow: follow-up-note
  version: "1.0.0"
  step: "4-build"
---

# Follow-Up Note

Generate a strategic post-conversation note for interviews, mentoring sessions, or networking calls. This skill is an advisor first, a note generator second — it leads with a strategic verdict on whether to send at all before writing anything.

## Required Inputs

- **Context type** — interview / mentoring / networking (infer from the conversation if not stated)
- **Who the conversation was with** — name, role, relationship to Nathan
- **What happened** — conversation notes, or the company file for interview rounds
- For interview: **which round** and **loop status** if known (optional; extracted from Cx file if available)

## Context Files (interview mode only)

| File | Path | What to extract |
|---|---|---|
| Cx | `context/companies/[slug].md` | Loop status, viability flags (comp, fit), interviewer profiles, debrief notes, what the interviewer revealed about their actual priorities |
| C7 | `context/search-constraints.md` | Comp floor and location requirements — used to assess loop viability |

For mentoring and networking mode, no context files are required — read from what Nathan provides.

## Style Rules (enforced across all modes and all drafts)

Non-negotiable:

- No em-dashes
- First name only — never "Hi Nathan Cho" or "Dear [Last Name]"
- One specific moment per note — not a summary of the whole conversation
- Banned phrases: "I wanted to reach out", "genuinely excited", "looking forward to connecting", "circling back", "touching base", "per our conversation", "as discussed", "I really enjoyed"
- No three-paragraph structure (opening paragraph / body paragraph / closing paragraph)
- No corporate sign-offs ("Best regards", "Sincerely", "Warm regards")
- Conversational close — sounds like something Nathan typed in 10 minutes, not assembled by a system
- The skill does not send anything — Nathan picks a draft and sends it himself

---

## Workflow

### Step 1 — Detect Context Type and Load Inputs

Determine the context type (interview / mentoring / networking) from what Nathan provided. If ambiguous, ask before proceeding.

**Interview:** Read the Cx company file if available. Extract: round type, interviewer name and role, loop status, viability flags, what the interviewer revealed about their actual priorities (not just the JD), and the engagement quality (warm and specific vs. transactional and procedural).

**Panel rounds:** If multiple interviewers appeared in the round, ask before generating: *"This round had [N] interviewers — should I generate a note for each, or focus on [decision-maker name]?"* If Nathan says all of them, generate one distinct note per interviewer, each anchored to something specific from that person's portion of the conversation. The 30/60/90 (if applicable) pairs with the decision-maker's note only.

**Mentoring and networking:** Read from Nathan's notes. Extract: who the person is, what they covered, any specific advice or insight that landed, and whether there's a natural next step.

---

### Step 2 — Appropriateness Analysis

Before generating any draft, output a strategic verdict. This is the skill's most important function.

**Assess across three dimensions:**

**1. Is there a real anchor?**
A real anchor is a specific moment from the conversation — something the person said that was non-generic, a reveal about their priorities, a point of genuine connection or intellectual engagement. Not a topic. Not "we discussed AI strategy." Something like: "she said the hardest part is that creative professionals can't express their quality bar as machine-learnable signal" or "he built a full PM coaching platform as his first coding project."

If there is no real anchor, the note will read as generic and the recipient will clock it. This is the single strongest signal for Not Appropriate or Borderline.

**2. What would this note actually accomplish?**
Be specific — not "keep the relationship warm" (generic). Something like: "this is the only chance to surface the architecture parallel that didn't fully land in the conversation" or "the accountability signal here is stronger than the gratitude angle — it tells him you'll actually act on what he said."

If the honest answer is social courtesy only — no candidacy impact, no relationship advance, no specific next step — name that explicitly in the verdict.

**3. How will the recipient likely perceive it?**
Predict based on the engagement quality and context. A warm, intellectually engaged interviewer who revealed their real priorities will read a specific note as attentive. A procedural, screening-mode interviewer will read even a good note as formulaic. Factor loop viability for interviews: if the loop has active flags that make it unlikely to proceed, a note changes nothing strategically.

**Verdict format:**

```
**Verdict: [Not Appropriate / Borderline / Send It]**

**What it would accomplish:** [1-2 specific sentences]

**How they'll likely perceive it:** [1-2 sentences — honest prediction]

[If Borderline: one sentence on what Nathan would gain by sending vs. skipping — frame it as his call]
[If Not Appropriate: one sentence on what would need to change for a note to make sense]
```

Stop here if Not Appropriate. Only proceed to Step 3 if Borderline or Send It.

---

### Step 3 — Identify Notable Moments

**Interview and networking modes:**

Scan the debrief notes or conversation for 2-3 genuinely notable moments. Criteria:
- Something the person spent disproportionate time on
- A reveal about their actual priorities that wasn't in the job description or obvious beforehand
- A point of genuine intellectual engagement or alignment
- Something unexpected that surfaced
- A concern or tension they named honestly

A notable moment is specific. "AI platform strategy" is not a moment. "He said the job is owning the layer that lets the advertising team build their own experience on top of what his team provides" is a moment.

If fewer than 2 notable moments exist, note this — it affects how many drafts to generate and may reinforce a Borderline verdict.

**Mentoring mode:** Skip this step. The note synthesizes the session rather than anchoring to a single extracted moment.

---

### Step 4 — Generate Drafts

**Interview mode:**

Generate one draft per notable moment (2-3 drafts total). Label each:

```
**Draft [A/B/C] — Anchored to: [the specific moment in plain language]**

[Draft text]
```

Each draft: 3-5 sentences. First name in the opening. The specific moment appears in the first or second sentence — not buried at the end. Conversational close. All style rules enforced.

**Mentoring mode:**

Generate one draft with this structure:

1. Opening sentence anchored to one specific piece of advice or insight that landed — not "great conversation" or a generic thank-you
2. 2-3 action item bullets — what Nathan will do with what he learned. These are the most strategically valuable part: they signal he was paying attention and will follow through. Keep them brief and specific (not a comprehensive session recap). Max 3 bullets.
3. 1-2 sentence close with a specific CTA — not "let's stay in touch" but something concrete: "would it be useful to check back in a few weeks after I've tried that framing?" or "happy to share what I find once I've dug into the framework you mentioned."

Total length: slightly longer than an interview note, still skimmable in under 30 seconds.

**Networking mode:**

Generate 1-2 drafts. Each: 3-5 sentences anchored to one specific thing the person said or offered. The close includes a soft but specific next step — not "would love to keep in touch" but something like "if you're open to it, I'd love an intro to [person they mentioned]" or "let me know if [topic] is useful to talk through — happy to return the favor."

---

### Step 5 — 30/60/90 Plan (interview mode, final round only)

**Generate only when ALL of the following are true:**
- The round is clearly a final round (or Nathan confirms it is)
- The interviewer is the decision-maker (VP, HM at offer stage, whoever is making the call)
- The loop does not have active viability flags that make it unlikely to proceed

**If there are viability flags (comp gap, strong fit concern, role viability unclear):** Surface this before generating: *"The debrief flagged [comp gap / fit concern] for this loop. Still want to generate the 30/60/90?"* Nathan decides.

**If the round is ambiguous:** Ask rather than assume — *"Is this the final round? If yes, I can generate a 30/60/90 to pair with the note."*

**The bridge sentence** (added to the selected note, not a separate document):

> "I put together a quick sketch of where I'd focus the first 90 days — based on what you said about [specific priority the interviewer revealed]. Happy to talk through it or ignore it entirely."

This sentence must reference something specific from the debrief — not "the role" or "our conversation" generically.

**The plan itself:**

Open with one framing sentence before any bullets — not a header, a sentence:

> "Based on what you described around [the interviewer's agenda item], here's how I'd orient the first three months — focused on [the tension or priority they named], not on a generic onboarding checklist."

Then three phases:

**30 days:** 2-3 bullets
**60 days:** 2-3 bullets
**90 days:** 2-3 bullets

Quality gate for each bullet: Can Nathan point to something the interviewer revealed in the debrief that grounds this bullet? If a bullet could have been written without the debrief, it doesn't belong. The plan should not be writable without the conversation intel.

Total length: readable in under 3 minutes. Delivered inline with the note — not as a separate attachment or PDF.

---

## Output Format

**If Borderline or Send It:**

```
**Verdict: [Send It / Borderline]**
**What it would accomplish:** [...]
**How they'll likely perceive it:** [...]
[Borderline: Nathan's call framing]

---

**Draft A — Anchored to: [moment]**
[Note text]

**Draft B — Anchored to: [moment]**
[Note text]

**Draft C — Anchored to: [moment]** (if applicable)
[Note text]

---

[30/60/90 section — interview mode, final round only]
*Add this sentence to whichever draft you choose:*
"[Bridge sentence]"

[Framing sentence]
30 days:
- [bullet]
- [bullet]

60 days:
- [bullet]
- [bullet]

90 days:
- [bullet]
- [bullet]
```

**If Not Appropriate:**

```
**Verdict: Not Appropriate**
**What it would accomplish:** [...]
**How they'll likely perceive it:** [...]
[What would change the verdict]
```

---

## Mode Reference

| Mode | Drafts | Appropriateness logic | CTA | 30/60/90 |
|---|---|---|---|---|
| Interview | 2-3 (one per notable moment) | Full analysis — round type, loop viability, engagement quality, anchor quality | Implicit / conversational close | Final round + decision-maker only |
| Mentoring | 1 (synthesizes session) | Almost always yes — focus is on what it accomplishes | Specific next step for the relationship | Never |
| Networking | 1-2 (one per notable thing) | Full analysis — anchor quality and whether a natural next step exists | Specific ask (intro, follow-up, resource) | Never |

---

## Style Examples

**Good interview note (specific anchor, conversational):**
> "Roei — thanks for the time today. Your framing at the close stuck with me: you know AI, the ad team knows advertising, and the job is owning the layer that lets them build their own experience. That's the problem I want to work on. Hope Austin has something soon."

**Bad interview note (generic, AI-sounding):**
> "Thank you so much for the wonderful conversation today about the AI Platform role at 6sense. I really enjoyed learning about the company's vision and am genuinely excited about this opportunity. Looking forward to hearing about next steps."

**Good mentoring action item (specific, accountable):**
> - Will use the "name the constraint before proposing the solution" framing in my Cisco round next week — happy to report back on how it lands

**Bad mentoring action item (vague):**
> - Will think more about my positioning and try to apply your advice going forward
