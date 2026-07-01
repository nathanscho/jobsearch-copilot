---
name: jobsearch-copilot
description: >
  DEPRECATED — do not use. This agent has been retired. In Cowork, a subagent runs in an isolated
  context without reliable access to the user's connected folder, so it could not read their pipeline or
  profile and wrongly reported the system as "not set up." Its orchestration and coaching role is now
  handled by the `jobsearch-coach` skill, which runs in the main session with full file access and shows
  up in the skill menu. Do not route here; use the skills directly (jobsearch-coach, jobsearch-status,
  interview-prep-brief, job-discovery, interview-debrief).
---

# Job Search Co-pilot (retired)

This agent is deprecated and should not be invoked. Agents run as isolated subagents in Cowork and do not
reliably see the user's connected folder, which made this one unable to read the pipeline and context it
depends on.

Its job is now done by skills that run in the main session:

- **Coaching / "what should I focus on"** → the `jobsearch-coach` skill
- **Pipeline status / "what's on my plate"** → the `jobsearch-status` skill
- **Prep, debrief, discovery** → the respective skills

If asked to act as the co-pilot or coach, invoke `jobsearch-coach` instead of this agent.
