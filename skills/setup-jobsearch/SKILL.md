---
name: setup-jobsearch
description: >
  This skill should be used when a new user is setting up the Job Search Co-pilot for the first time,
  or wants to reconfigure it. Triggers on "set up job search", "set up the job search co-pilot",
  "onboard me", "get started with job search", "configure my job search", or when any other
  job-search skill reports that config.md or the context files are missing. Bootstraps the user's
  context from their resume (auto-drafting the candidate profile and seeding starter stories), runs a
  short resume-informed Q&A for the forward-looking pieces a resume can't supply (target role,
  constraints, gaps), writes config.md and the context files, and routes the user to their first prep
  brief. Offers an Express (resume-only) or Guided path.
metadata:
  version: "1.3.0"
---

# Setup — Job Search Co-pilot

Onboard a new user from zero to first value as fast as possible. The skills in this plugin are generic;
everything personal lives in the user's `config.md` and context files. The fastest path to value is a
prep brief, which needs only the user's resume plus a little forward-looking context — so this setup is
built around the resume, not a long questionnaire.

Write all output in plain language. Do not expose internal paths or schema unless asked.

## Minimum viable context

The only file the user must provide is their **resume**. From it, draft the candidate profile (C2) and
seed a few stories (C1). A short Q&A adds the forward-looking pieces a resume can't contain. Everything
else (loop log C6, intelligence C8, mock diagnostics C4, pipeline state) fills itself in automatically
as the user runs the other skills. The target company map (C3) gets a lightweight starter seed during
Guided setup (Step 4c) rather than waiting entirely on job-discovery. Never block the user on files that
accumulate through use.

## Prerequisites

The user needs a folder connected in Cowork to hold their job search. If none is connected, ask them to
connect one before continuing (this becomes their `workspace_path`).

## Workflow

### Step 1 — Create structure and copy templates

Confirm the connected folder. Inside it, create:

```
context/
context/companies/
documents/prep-briefs/
documents/debriefs/
Recordings & Transcripts/Company Interviews/
```

Locate this plugin's templates at `../../templates/` relative to this skill's own directory — the base
directory shown when this skill loads is `<plugin-root>/skills/setup-jobsearch/`, so templates are at
`<plugin-root>/templates/`. Copy `<plugin-root>/templates/context/`*.md into the user's `context/`, and
copy `<plugin-root>/templates/config.example.md` to `context/config.md`. If the templates can't be
located, don't stop — create equivalent files from the structures in this plugin's `README.md` and
`CONNECTORS.md`.

### Step 2 — Choose a path

Offer two options (AskUserQuestion):

- **Express** — "Just point me at your resume and I'll get you to a first prep brief in a couple
  minutes." Runs Step 3, then skips to Step 6.
- **Guided (recommended)** — "Resume plus about six quick questions, for a sharper profile and to turn
  on job discovery." Runs Steps 3, 4, 5, 6.

### Step 3 — Resume bootstrap (both paths)

1. Ask for the resume file and record its location as `resume_path` in `config.md`.
2. Read the resume. Draft `context/candidate-profile.md` (C2) using the template's active-voice
   structure: a short positioning statement (who they are, what they're known for, what they're
   optimizing for right now), and 2-3 **target job profiles** — each a distinct class of role they're
   credibly going after, with its own pitch, proof points drawn from the resume, what differentiates
   them from a typical candidate for that profile, and any watch-out/gap to manage. Don't write this as
   a passive analysis of the candidate — write it as the active positioning case for each profile, in
   the confident, specific voice the candidate would use themselves.
3. Seed `context/story-bank.md` (C1) with 3-5 candidate stories drawn *only* from what the resume actually
   states, in the story arc (Hook → Stakes → Tension → Judgment → Impact → Lesson), tagged by type. Mark
   any missing element as a prompt to fill later — never invent detail to strengthen a story.
   `story-bank-builder` will develop these fully.
4. Show the drafts back and let the user correct. Frame it as confirmation, not authorship: "Here's how
   I'd position you based on your resume — what's off, and which of these profiles feels most like the
   right lead?"

Resume-only is enough to generate a usable first brief. The Q&A below makes it strong.

### Step 4 — Guided Q&A (Guided path only)

Ask only what the resume cannot tell you. Propose answers from the resume where possible so the user is
confirming, not generating cold. Keep it to ~6 questions, one topic at a time:

1. **Target role and level next** — what they want now (propose from resume seniority). Use this to
   sanity-check the job profiles drafted in Step 3.
2. **Why now / what they're optimizing for** — the search thesis.
3. **Sharpen differentiators** — confirm the resume-derived ones and add anything the resume undersells.
4. **Hard constraints (C7)** — comp floor, location/remote, level floor, dealbreakers, industry exclusions.
5. **Known target companies** — any companies already on their radar, even informally. This is
   low-friction extra signal: if they name any, note which job profile each best fits and carry them
   straight into Step 4c instead of starting the company map from scratch.
6. **Biggest gap** an interviewer will probe, and their honest answer.

Write the role/thesis/positioning/gaps into `context/candidate-profile.md` (C2) and the constraints into
`context/search-constraints.md` (C7). Confirm before writing.

### Step 4b — Deepen positioning and stories (Guided, recommended)

Two optional but high-value steps that turn a thin cold-start profile into a sharp one:

- **Sharpen positioning** → run `positioning-thesis`. Have the user share a few target job links; it maps
  the real demand, proposes 2-3 positioning profiles, and surfaces adjacent roles they're qualified for
  but haven't considered. Updates C2 — reconcile against the job profiles drafted in Step 3 rather than
  replacing them outright.
- **Build out stories** → run `story-bank-builder`. It finds the gaps in their story coverage and
  interviews them to fill the strongest ones — extracting real detail, never inventing. Builds C1.

Offer both; recommend at least `positioning-thesis`, since a sharp C2 improves every prep brief. The user
can also skip straight to a first brief and do these later.

### Step 4c — Seed the target company map (Guided path)

Don't leave `context/target-company-map.md` (C3) empty until job-discovery runs. Seed a lightweight
starter list now, organized by the job profiles from Step 3:

1. For each job profile in C2, propose 2-4 target companies that fit — starting with any companies the
   user named in Step 4, then filling gaps with companies that plausibly match the profile's domain and
   the user's constraints (C7: location/remote, comp floor, industry exclusions).
2. Tag each company with the job profile it maps to, a one-line fit angle, and a priority tier
   (Priority 1/2/3 per the template).
3. Where feasible, do a quick check (e.g. a web search) on basic facts like headquarters/remote policy,
   or whether a role matching the profile appears to be currently open — note in the company's entry
   when something is directional/unverified rather than confirmed, so the user knows what to double
   check before investing outreach time.
4. Show the starter map back to the user briefly and let them correct or re-tier before moving on.

This step is what makes C3 useful from day one instead of only accumulating through job-discovery.

### Step 5 — Connectors and config (Guided path)

Fill the rest of `config.md`. Use AskUserQuestion for connector choices:

- **Email connector (required for job-discovery and status):** which email tool they've connected (Gmail,
  Outlook). Also ask what sends their job-alert digest (`job_alert_sender`); if none yet, note discovery
  needs one and they can add it later.
- **Chat connector (optional):** Slack/Teams for posting and tracking pipeline updates. If yes, get the
  channel ID; if no, leave blank — everything works without it.
- **Files connector (optional):** Drive/Box to also upload finished briefs/debriefs. If yes, get folder
  IDs; if no, leave blank — briefs stay local.

(Express path: skip — email can be added later, only needed when they first run job discovery.)

### Step 6 — First value

Route the user straight to a win:

> "You're set. Want to generate your first prep brief now? Paste a job description, the interviewer's
> name/role, and the interview date, and I'll build it." (interview-prep-brief)

If they don't have an interview lined up, suggest `run job discovery` (Guided users with email connected)
or building out more stories with story-bank-builder. If Step 4c ran, mention the starter target company
map is ready and can guide outbound networking even before job-discovery is connected.

### Step 7 — Offer add-ons

1. **The co-pilot agent** — one orchestrator across the funnel (discover → prep → interview → debrief →
   retro) that reads pipeline state and suggests the next action. Recommend enabling once they're
   comfortable with the individual skills.
2. **Daily chat digest (optional, needs a chat connector)** — a scheduled morning task that runs
   job-discovery + jobsearch-status and posts a digest. See `<plugin-root>/addons/daily-digest.md`.

## Notes

- Never write personal data into the plugin's own files — only into the user's workspace folder.
- Reconfiguring (files already exist): confirm before overwriting; update in place where possible.
- Always prefer getting the user to a first prep brief quickly over completing every context file.
- Candidate profile and target company map should stay in sync: if a job profile's target companies
  change in C3, or a new profile gets added in C2, update the other file to match.
