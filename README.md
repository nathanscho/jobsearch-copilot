# Job Search Co-pilot

A role-fit reasoning system for high-stakes job searches.

Most job-search tools help you move faster: tailor resumes, generate cover letters, apply to more roles.
This one is built around a different philosophy:

> Do not make hiring teams connect the dots.

Job Search Co-pilot helps you understand what a role is really hiring for, map your experience honestly,
form a clear positioning thesis, prepare for interviews, debrief what happened, and improve across the
full loop.

It is not an auto-apply bot.
It is a thinking system for candidates who want quality, fit, and clarity.

## Who this is for

This is designed for senior PMs and similar knowledge-worker roles where success depends on more than
keyword matching.

It is especially useful if you are trying to:

- Clarify your positioning across multiple target roles
- Understand whether a role is actually a strong fit
- Prepare for interviews with a sharper point of view
- Build a reusable story bank
- Debrief real interviews and extract forward guidance
- Diagnose mock interview performance
- Track patterns across a job-search loop

The current setup is optimized around senior product management searches, but the underlying skills can
be adapted to other roles.

## Core idea

A strong candidate does not just answer questions well.

A strong candidate helps the interviewer understand:

- What problem the role is likely hiring for
- Why their background maps to that problem
- Where there may be legitimate risks or gaps
- What examples best prove fit
- What questions should be asked to test mutual fit

The goal is not to fake certainty. The goal is to turn scattered experience into a clear, evidence-backed
role-fit thesis.

## What it helps you produce

Depending on the skill you run, the system can help create:

- A candidate profile
- A target-role positioning thesis
- A story bank
- A curated job shortlist
- A pipeline/status view
- Interview prep briefs
- One-page interview cheat sheets
- Interview debriefs
- Mock interview diagnostics
- Cross-loop coaching and retrospectives

The system gets sharper over time because it accumulates context from your profile, stories, constraints,
interview notes, pipeline, and debriefs.

## Quick start

1. Install the plugin in Cowork:
   - Open **Customize**
   - Go to **Plugins**
   - Open **Personal plugins**
   - Click **+**
   - Choose **Add marketplace**
   - Choose **Add from a repository**
   - Enter `nathanscho/jobsearch-copilot`
   - Install the `jobsearch-copilot` plugin
2. Connect a folder in Cowork to hold your job-search context.
3. Say:
   ```text
   set up the job search co-pilot
   ```
4. Provide your resume.
5. Choose a setup path:
   - **Express:** resume-only setup, fastest path to value
   - **Guided:** resume plus a few questions about your goals, constraints, target companies, and
     perceived gaps
6. Generate your first prep brief by pasting:
   - Job description
   - Company
   - Interview round
   - Interviewer, if known
   - Interview date, if known

The fastest useful path is:

```text
resume → confirm candidate profile → generate first prep brief
```

## Golden path

If you are new, start here:

1. **Set up the co-pilot** — builds your initial profile and context files from your resume.
2. **Run a positioning thesis** — helps clarify the types of roles you should target and how to explain
   your fit.
3. **Build or refine your story bank** — turns your background into reusable evidence for interviews.
4. **Generate an interview prep brief** — converts a role into a specific interview strategy.
5. **Debrief after each real interview** — captures what happened, what signal you got, and what to
   adjust next.
6. **Run coaching periodically** — looks across the full search for patterns, blindspots, and next
   actions.

## Minimum viable context

You do not need to fill out everything manually. The only thing you need to start is your resume.
Everything else can be drafted, asked during setup, or accumulated as you use the system.

| Context | How it gets filled | Used for |
| --- | --- | --- |
| Resume | You provide it | Fast first prep briefs |
| Candidate profile | Drafted from your resume, then confirmed | Positioning and interview prep |
| Story bank | Seeded from your resume, then expanded | Behavioral and leadership interviews |
| Search constraints | Asked during setup | Job discovery and prioritization |
| Target company map | Seeded during guided setup | Networking and role targeting |
| Loop logs | Built from debriefs | Pattern recognition |
| Mock diagnostics | Created from practice interviews | Coaching and skill development |
| Pipeline state | Synced from email and optional chat | Search status and next actions |

The system is useful on day one, but becomes more valuable after each prep, debrief, and diagnostic.

## Skills

| Skill | What it does |
| --- | --- |
| `setup-jobsearch` | One-time onboarding. Creates your config and context files. |
| `positioning-thesis` | Analyzes target JDs and proposes target job profiles, pitch, differentiation, target companies, and adjacent-fit blindspots. |
| `story-bank-builder` | Finds gaps in your story coverage and interviews you to fill them. Never fabricates. |
| `job-discovery` | Screens job alerts into a curated shortlist. |
| `jobsearch-status` | Syncs email, plus optional chat, into a current pipeline view. |
| `interview-prep-brief` | Creates a tailored prep brief and one-page cheat sheet for a specific round. |
| `interview-debrief` | Scores a completed round and extracts forward guidance, from your notes or a transcript if you have one. |
| `diagnose-mock-interview` | Diagnoses mock or practice answers. Not intended for real interview debriefs. |
| `jobsearch-coach` | Acts as a reflective coach across goals, patterns, blindspots, accountability, funnel health, and positioning. |
| `market-pulse` | Scans your watchlist for changes and surfaces engagement openings. Never drafts or sends. |
| `engagement-sync` | Reconciles thread state against your LinkedIn inbox and scores who to engage next. Never drafts or sends. |
| `content-draft` | Drafts LinkedIn posts and comments, grounded in your scope boundaries, thread state, and current facts, gated by the fact-checker agent before it's presented as ready to ship. |

To get coaching, say something like:

```text
coach me
```

or:

```text
what should I focus on next?
```

(An earlier `jobsearch-copilot` *agent* was retired: agents run isolated from your folder in Cowork and
couldn't reliably read your pipeline. `jobsearch-coach` replaces it.)

## Optional add-on

`addons/daily-digest.md` — a scheduled morning digest that can be posted to your chat channel. This
requires a chat connector.

## Personalization model

The skills in this repo are generic. Your personal job-search data lives in your own connected folder and
tools, never in this repo.

| File | Purpose |
| --- | --- |
| `context/config.md` | Paths, job-alert source, and which connectors you use |
| `context/story-bank.md` (C1) | Your reusable interview stories |
| `context/candidate-profile.md` (C2) | Your candidate profile and positioning |
| `context/target-company-map.md` (C3) | Target companies and role categories |
| `context/mock-diagnostics-log.md` (C4) | Practice interview diagnostics |
| `context/interview-loop-log.md` (C6) | Interview loop notes and debrief history |
| `context/search-constraints.md` (C7) | Role preferences, constraints, and search criteria |
| `context/jobsearch-intelligence.md` (C8) | Company, role, and interview intelligence |
| `context/coaching-log.md` (C9) | History of coaching check-ins and commitments |
| `context/companies/[slug].md` (Cx) | Per-company file: prior rounds, interviewer intel |
| `context/pipeline-state.md` | Current job-search pipeline state |

Templates for these files live in `templates/` and are copied into your folder during setup.

## Connectors

See `CONNECTORS.md`. No connectors are required to get started, positioning, story bank, prep briefs,
debriefs, and coaching all work with just your resume and Cowork itself. Connect these when you want more
automation:

- Email connector, to unlock job discovery and automated pipeline status
- Chat connector, for digests and chat-based search updates
- File connector, for uploading finished prep briefs and debriefs

If a connector is missing, the skills that need it aren't available yet; everything else works normally.

## Data and privacy

Your personal data stays in your own environment. That includes:

- Resume
- Candidate profile
- Story bank
- Search constraints
- Pipeline
- Interview notes
- Email access
- Chat access
- Files

None of your personal data is sent back to the plugin author. This repo contains generic skills and
templates only — it does not include anyone else's private job-search data.

## What this is not

This is not a tool for:

- Mass-applying to jobs
- Spamming recruiters
- Fabricating experience
- Keyword-stuffing resumes
- Outsourcing judgment to AI
- Pretending every role is a fit

The system is intentionally built around human judgment. You own the truth, the strategy, and the final
voice. The co-pilot helps structure the thinking.

## Example prompts

Set up the system:

```text
set up the job search co-pilot
```

Create a positioning thesis:

```text
Analyze these target roles and help me refine my positioning thesis.
```

Build the story bank:

```text
Review my story bank and find the biggest gaps for senior PM interviews.
```

Prepare for an interview:

```text
Create an interview prep brief for this role.
```

Debrief a real interview:

```text
Debrief this interview and tell me what signal I should take from it.
```

Diagnose a mock interview:

```text
Diagnose this mock answer. Separate navigation issues from judgment issues.
```

Get coaching:

```text
Coach me on what I should focus on next in my search.
```

## Design principles

1. **Fit over volume** — the goal is not to apply to more jobs. The goal is to identify and pursue roles
   where there is a credible fit.
2. **Evidence over vibes** — positioning should be grounded in real experience, real stories, and real
   role requirements.
3. **Clarity over completeness** — interviewers should not have to assemble your fit from scattered
   examples.
4. **Human judgment over automation** — the co-pilot can suggest, structure, and challenge. It should not
   invent or decide for you.
5. **Learning loop over one-off prep** — each prep, mock, and debrief should improve the next one.

## License

MIT
