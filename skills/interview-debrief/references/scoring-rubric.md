# Interview Scoring Rubric

*Read this file before scoring in Step 2. Score against these behavioral descriptions — not against other rounds the user has done, and not against the model's implicit sense of "good." Transcript excerpts are ground-truth anchors: real the user moments at a validated score level.*

---

## Score scale

| Score | Label | Meaning |
|---|---|---|
| 5.0 | Exceptional | Proactively drove this dimension without prompting |
| 4.0 | Strong | Demonstrated clearly and held up under probing |
| 3.0 | Solid | Met the bar but required at least one prompt, or had a notable gap |
| 2.0 | Weak | Below bar — vague under probing, or meaningfully missed the dimension |
| 1.0 | Significant gap | Dimension was absent or collapsed entirely |

Halves (1.5, 2.5, 3.5, 4.5) interpolate between adjacent anchors.

**Senior PM calibration (applies to all dimensions):** Impact scope should be cross-team or business-level, not personal or single-team. A story that would be a 4.0 for a junior PM is a 3.0 for a senior PM if the scope is only personal or local.

---

## Recruiter screens

Score only **Clarity**, **Positioning alignment**, and **Conviction**. Mark Depth and Adaptability as **N/A**. Avg = mean of the 3 scored dimensions only.

---

## DIMENSION 1: DEPTH

*What it measures: Does the user demonstrate real PM judgment — not just what happened, but why it mattered, what trade-offs were involved, what they'd do differently? Do they drive specificity unprompted, or wait to be asked?*

*Depth vs. Adaptability distinction: Depth measures whether the substance was there when the right question was asked. Adaptability measures whether the user got to the right question efficiently.*

---

### Analytical / Metrics rounds

*Source: Lenny's Newsletter analytical thinking rubric (Ben Erez, ex-Meta PM). What interviewers test: can the user set goals and analyze data in a structured way? Can they define metrics specific enough for a data scientist to implement?*

**5.0 — Exceptional**
- Scoped and stated assumptions unprompted before starting
- Built ecosystem-level thinking: identified all stakeholders and their value exchange, not just the obvious user
- Defined NSM with a time frame AND proactively critiqued its own failure modes (what could make this metric go up while the product fails)
- Made the altitude shift from product-level metrics to team-level goals without being asked
- All metrics are implementable — specific enough that a data scientist could write a query

**4.0 — Strong**
- Stated assumptions upfront; built a reasonable ecosystem view
- NSM defined with time frame; held up when probed on "why this metric vs. alternatives"
- Could explain metric trade-offs when asked

**3.0 — Solid**
- Got to the right answer with some guidance; required at least one prompt to reach specifics
- Metrics directionally correct but vague (e.g., "engagement" without a time frame)
- NSM logic defensible but didn't address guardrails until asked

**2.0 — Weak**
- Required 2+ redirects before reaching the right analytical frame
- Metrics were generic or couldn't be queried
- Defaulted to technical/data-layer diagnosis before business diagnosis

**1.0 — Significant gap**
- Failed to reach a structured analytical answer even with prompting
- Couldn't name specific metrics or defend a North Star choice at all

---

### Behavioral / Individual leadership rounds

*Source: Tech Interview Handbook (ex-Meta EM); STAR-L framework (Google). What interviewers test: does the story hold up under multi-layer probing? Does it show learning — what changed — not just execution?*

**5.0 — Exceptional**
- Story demonstrates org-level or cross-team impact (multiple teams or business-level outcome)
- Includes unprompted "L" (learnings) — what specifically changed in how the user works as a result
- Defends every claim with specific data or mechanism when pushed
- Acknowledges counterarguments or what they'd do differently
- Story complexity matches senior PM bar (cross-team scope, not just personal win)

**4.0 — Strong**
- Cross-team or significant team-level impact; outcome is specific and measurable
- Story holds up under one round of probing with specific data
- Learnings present when asked; concrete, not generic

**3.0 — Solid**
- Team-level impact; outcome is directionally specific but missing a key detail (metric, mechanism, or scope)
- Holds up under shallow probing; starts to thin when pushed further
- Learnings are vague or generic ("I learned to communicate better")

**2.0 — Weak**
- Story is about activity, not impact; or impact is asserted without evidence
- When probed, retreats to generalities rather than specifics
- No genuine learnings — or "learnings" section is an advocacy story rather than a growth story

**1.0 — Significant gap**
- Story collapses under first follow-up
- Can't substantiate the action or result with any specifics
- Story is about someone else's contribution or is missing a clear Task/Action/Result

---

### Product sense / HM screen rounds

*What interviewers test: can the user think at platform/ecosystem level before jumping to solutions? Do they establish a strategic thesis before proposing features?*

**5.0 — Exceptional**
- Led with platform-level strategic frame before proposing solutions (flywheel, ecosystem, business model)
- Identified non-obvious stakeholders and their trade-offs
- Solutions tied back to the strategic frame, not generated independently
- Demonstrated product intuition about why this problem matters now

**4.0 — Strong**
- Strategic frame present; solutions follow from it
- Depth under probing is solid; can explain "why this solution vs. alternatives"

**3.0 — Solid**
- Reasonable product thinking; some framework visible
- Solutions are plausible but not tied to a strategic thesis
- Depth requires one prompt to surface

**2.0 — Weak**
- Feature-level thinking; jumped to solutions without strategic framing
- When probed on "why this," answer is circular or generic
- Story selection doesn't match the complexity the round is testing

**1.0 — Significant gap**
- No strategic frame; solution-first without user or business grounding
- Can't explain trade-offs or why this product decision over alternatives

---

### Engineering collaboration rounds

*What interviewers test: can the user work as a peer with engineers, not just a spec-writer? Do they understand the technical substance of their own products?*

**5.0 — Exceptional**
- Demonstrated technical depth at peer level: architecture, trade-offs, implementation constraints
- Named specific mechanisms, not just outcomes
- Showed PM judgment on technical decisions: "we chose X over Y because of Z constraint"

**4.0 — Strong**
- Technically credible; held up on domain-specific questions
- PM contribution to technical decisions was clear

**3.5 — Solid-plus**
- Technically adequate; answered domain questions correctly; hotel rescue or similar story showed PM-led technical rescue with specific outcome

**3.0 — Solid**
- Technically adequate; answered domain questions correctly
- PM-engineering collaboration model was described clearly
- Depth required at least one probe to surface

**2.0 — Weak**
- Technical answers were shallow or avoided specifics
- Collaboration model described at process level ("I work closely with engineers"), not substance level ("here's how I made the specific trade-off call")

**1.0 — Significant gap**
- Couldn't engage on technical substance; deferred to "I'd ask the engineers" without demonstrating prior technical judgment

---

### GTM / Sales collaboration rounds

*What interviewers test: does the user understand the commercial side of the product — pricing, competitive dynamics, deal mechanics, buyer needs?*

**5.0 — Exceptional**
- Background directly mapped to the specific commercial problems the interviewer faces
- Demonstrated understanding of buyer, deal mechanics, and competitive landscape at a specific level
- Added insight the interviewer hadn't considered

**4.0 — Strong**
- Commercially aware; understood key deal dynamics and customer needs
- Substantive conversation about GTM motion without needing to fill in context

**3.0 — Solid**
- Adequate commercial understanding; some gaps in deal-level specifics
- Useful conversation but interviewer had to provide some context

**2.0 — Weak**
- Generic commercial framing; couldn't speak to specifics of this company's market or buyer
- Collaboration model was process-level, not substance-level

**1.0 — Significant gap**
- No commercial awareness; couldn't engage on deal, pricing, or competitive dynamics

---

## DIMENSION 2: CLARITY

*What it measures: Were answers structured and easy to follow? Did the user signal structure upfront and follow it?*

**5.0** — Stated structure before starting ("I'll cover three things: X, Y, Z"); followed it; interviewer never had to ask "what are you getting at?"

**4.0** — Clearly organized and easy to follow; one minor instance of losing the thread, recovered.

**3.0** — Reasonably clear; some answers ran long or required the interviewer to re-orient; didn't always signal structure upfront.

**2.0** — Verbose or meandering; interviewer redirected for focus more than once; logic arc hard to follow.

**1.0** — Unclear throughout; interviewer had to interpret or reconstruct the answer.

---

## DIMENSION 3: POSITIONING ALIGNMENT

*What it measures: Did answers reinforce the user's target narrative (from C2)? Did they connect their experience to this company's specific needs — not just describe their background accurately?*

**5.0** — Positioning landed precisely; interviewer reflected the framing back. the user explicitly connected their background to the company's strategic thesis.

**4.0** — Strong connection between the user's background and the role; interviewer engaged at depth with the positioning. No disconnect raised.

**3.0** — Positioning was reasonable but generic; didn't connect tightly to this company's specific problem. Could have been said to any company in the category.

**2.0** — Positioning missed the company's actual bar or domain; the user described their background accurately but didn't translate it to why it matters here specifically.

**1.0** — Active positioning mismatch; the user's framing contradicted what the company was looking for.

---

## DIMENSION 4: ADAPTABILITY

*What it measures: Did the user respond well to follow-ups, pivots, and unexpected questions? Did they recover when off-balance?*

**5.0** — Followed the interviewer's pivots naturally; conversation felt like a peer exchange; unexpected questions handled without visible recovery effort.

**4.0** — Handled follow-up probes cleanly; one moment of recalibration but recovered well and closed positively.

**3.0** — Generally adaptive; one notable stumble or redirect that required visible effort to recover from.

**2.0** — Struggled to adjust when redirected; kept returning to the original answer frame rather than following the interviewer.

**1.5** — Recovery attempt backfired; trying to fix a weak answer in Q&A reinforced the gap.

**1.0** — Couldn't adapt at all; remained in the wrong frame throughout despite multiple redirects.

---

## DIMENSION 5: CONVICTION

*What it measures: Were answers delivered with confidence? Did the user defend positions when pushed, or soften without a principled reason?*

**5.0** — Confident throughout; defended positions with specific reasoning when challenged; didn't soften under social pressure without a substantive counter-argument.

**4.0** — Generally confident; one moment of softening under challenge but recovered to a principled position with reasoning.

**3.0** — Adequate conviction; some hedging; positions were held but delivery didn't project strong confidence throughout.

**2.5** — Disclosed information that undermined the conviction signal; enthusiasm present but undercut by a framing risk.

**2.0** — Conviction visibly dropped when challenged; answers hedged or retreated without a principled reason.

**1.0** — Answers so hedged they didn't communicate a view; or reversed positions immediately under light challenge.

---

## Rubric maintenance

Add new anchors after validated debriefs: when a transcript excerpt clearly exemplifies a score level and the user confirms the score, add it here in the relevant section. Format: `*Anchor — [Interviewer] ([Round type], [Date], score [X.X]): [2-3 sentence description of what specifically happened.]*`

Do not add anchors from AI-inferred scores alone. An anchor is only valid if the user has confirmed the score as accurate.

*Last updated: 2026-06-23 | Sources: Lenny's Newsletter analytical thinking rubric (Ben Erez, ex-Meta); Tech Interview Handbook behavioral rubrics (ex-Meta EM)*
