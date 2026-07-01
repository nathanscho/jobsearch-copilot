# Job Search Co-pilot

A personalized job-search system for senior PMs and similar roles. It discovers roles, prepares you for
interviews, debriefs completed rounds, diagnoses mock interviews, and runs cross-loop retrospectives.

The skills are generic. Everything personal — your profile, stories, constraints, and connectors —
lives in **config + context files** in your own folder. That means you and anyone you share this with
run the exact same skills against your own data.

## Quick start

1. Install the plugin.
2. Connect a folder in Cowork to hold your search.
3. Say **"set up the job search co-pilot."** Setup is built around your resume: it reads your resume,
   drafts your candidate profile — including 2-3 target job profiles with their own pitch and target
   companies — and a few starter stories, then asks a handful of quick questions for what a resume can't
   tell it (what you want next, your constraints, target companies already on your radar, your biggest
   gap). Pick **Express** (resume only, ~2 min) or **Guided** (resume + ~6 questions, sharper, ~5 min).
4. Generate your first prep brief: paste a job description, the interviewer, and the date.

## Minimum viable context (fastest path to value)

You don't need to fill out everything to get value. The only thing you must provide is your **resume** —
everything else is either drafted from it, asked in a 5-question setup, or accumulated automatically as
you use the tool.

| Context | How it gets filled | Needed for |
| --- | --- | --- |
| Resume | You provide the file | Prep briefs (the fast first win) |
| Candidate profile / stories | Auto-drafted and seeded from your resume, you confirm | Prep briefs |
| Search constraints | 6-question setup | Job discovery |
| Target company map | Lightweight starter seed during Guided setup, organized by target job profile | Networking + job discovery |
| Loop log, intelligence, mock diagnostics, pipeline | Fill in automatically as you run debriefs, retros, and discovery | Later-stage value |

So the smallest useful start is: **resume → confirm the auto-drafted profile → first prep brief.** The
system gets sharper the more you use it.

## What's inside

**Skills**

| Skill | What it does |
| --- | --- |
| `setup-jobsearch` | One-time onboarding — creates config + context files |
| `positioning-thesis` | Analyzes your target JDs → proposes 2-3 target job profiles (pitch, differentiation, target companies each) + exposes adjacent-fit blindspots (builds C2, and C3 if companies surface) |
| `story-bank-builder` | Finds gaps in your story coverage and interviews you to fill them — never fabricates (builds C1) |
| `job-discovery` | Screens your job-alert digest into a curated shortlist |
| `jobsearch-status` | Syncs email (+ optional chat) into a current pipeline view |
| `interview-prep-brief` | A tailored 3-part prep brief + one-page cheat sheet per round |
| `interview-debrief` | Scores a completed round and extracts forward guidance |
| `diagnose-mock-interview` | Coaching on practice/mock answers (not real rounds) |
| `jobsearch-coach` | Your reflective coach — patterns, blindspots, accountability, goals, what to focus on, plus a periodic deep review (funnel + positioning) |

**On the "coach" / "what should I do next":** just say "coach me" or "what should I focus on" and the
`jobsearch-coach` skill runs in your main chat. (An earlier `jobsearch-copilot` *agent* was retired —
agents run isolated from your folder in Cowork and couldn't read your pipeline. The skill replaces it.)

**Add-on (optional, needs a chat connector)**

`addons/daily-digest.md` — a scheduled morning digest posted to your chat channel.

## Personalization model

- `context/config.md` — paths, job-alert source, and which connectors you use.
- `context/*.md` — your candidate profile (C2), story bank (C1), search constraints (C7), target
  company map (C3), and logs that accumulate as you go (C4/C6/C8, pipeline-state).
- Templates for all of these ship in `templates/` and are copied into your folder during setup.

## Connectors

See `CONNECTORS.md`. Only an email connector is required; chat and files are optional conveniences the
skills skip cleanly when absent.
