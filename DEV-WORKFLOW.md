# Dev workflow — jobsearch-copilot

This plugin is distributed straight from this GitHub repo via a Cowork/Claude Code plugin
marketplace (`.claude-plugin/marketplace.json`, plugin source `github: nathanscho/jobsearch-copilot`).
There is no separate build step and no `.plugin` bundle file anymore — this repo *is* the
release artifact.

## Three places this plugin "lives," and how they relate

1. **Workshop — this folder.** Where all editing happens, always. Nothing here is "live"
   anywhere else until it's pushed.
2. **GitHub — this repo's commit/tag history.** The version-controlled record. Pushing a
   commit doesn't automatically mean anyone's Cowork picks it up (see below) — it just means
   the change now exists somewhere durable and reviewable.
3. **Consumption points — each syncs from GitHub independently, not from the Workshop:**
   - **Your own Cowork "Personal plugins" install** — powers manual `/jobsearch-copilot:*`
     invocations in chat. Reflects whatever was on GitHub the last time you refreshed the
     marketplace in Cowork, not your latest unpushed edits.
   - **Your scheduled tasks** — deliberately bypass all of this and read skill files directly
     from the Workshop path. They always run your current local state, released or not. This
     is intentional: unattended automation shouldn't depend on marketplace sync timing.
   - **Anyone else's Cowork install** (friends testing this) — same as your own personal
     install: syncs from GitHub, never sees the Workshop.

## Operating model

### 1. Discovering gaps

Gaps surface from three places: your own real usage of the installed plugin (see "Workshop vs.
installed" below), the scheduled tasks' daily output, or feedback from friends using their own
install. When you notice one, don't fix it inline mid-task. Open a **GitHub Issue** on this repo
(github.com/nathanscho/jobsearch-copilot → Issues → New issue). This is the backlog, one place,
visible to you and to friends, and public issues let friends report their own gaps directly
instead of routing everything through you.

### 2. Suggesting improvements

Triage issues in batches rather than one at a time. For each: write the fix as a short spec in
the issue itself (what's wrong, what the fixed behavior should be) before touching code, this is
usually a sentence or two. For anything that touches how multiple skills read/write the same
context files (C1–C7), check downstream consistency first — a schema change in one place often
needs matching edits across several SKILL.md files.

### 3. Testing

Edit in the Workshop, then validate **before** releasing by asking Claude to run the skill
directly against the local file path, e.g. "run the updated
`skills/job-discovery/SKILL.md` against my real pipeline" — same mechanism the scheduled tasks
use. This is real data, not fixtures, so for a change that *writes* to your context files
(job-discovery, jobsearch-status, jobsearch-coach), review the diff before confirming the write.
Your `context/` files live in the outer Playground repo, which is also git-tracked, so a bad
write is recoverable with `git diff` / `git checkout` there too, but it's cheaper to just look
before you write.

For a genuinely large or risky change (schema rework, cross-skill refactor), do it on a `dev`
branch and merge to `main` once it's proven out. For a normal small fix, working straight on
`main` is fine, you're the sole maintainer for now.

### 4. Pushing the refinement to GitHub

Once validated:
- Bump `version` in `.claude-plugin/plugin.json`.
- `git add -A && git commit -m "Fixes #<issue number> — <what changed>"`
- Tag it to match: `git tag vX.Y.Z`
- `git push && git push --tags`
- Close the GitHub issue (referencing "Fixes #N" in the commit message does this automatically
  once it's on `main`, or close it manually).
- In Cowork: Personal plugins → find `jobsearch-copilot-marketplace` → refresh/re-add if it
  doesn't auto-pick-up the new version → reinstall/update the plugin. Removing and re-adding the
  marketplace has been the most reliable way to force a fresh pull so far.

## Workshop skills vs. installed `/jobsearch-copilot:*` skills

Use the **installed marketplace skill** (`/jobsearch-copilot:job-discovery`, etc.) for all real
usage, actually running your job search day to day. This is the released, stable version, the
same one friends are running, so using it yourself is also your best ongoing check that releases
actually work.

Use the **Workshop direct-path skill** (asking Claude to run the local `SKILL.md` file directly)
only in one situation: you just edited something and want to validate the edit before it's
released. It will never be what you reach for during normal usage, only during the testing step
above.

Rule of thumb: if the goal is "get my job search done," use the installed skill. If the goal is
"did my edit work," use the Workshop path.

## Reverting a bad release

Every release is tagged (`vX.Y.Z`), so you always have a clean rollback point instead of
hunting through raw commits:

```bash
# see all releases
git tag

# inspect an old one without losing current work
git show v1.6.0:.claude-plugin/plugin.json

# roll the whole working tree back to a known-good tag
git checkout v1.6.0 -- .
git commit -m "Revert to v1.6.0 — <reason>"
git tag v1.6.2   # next version number, don't reuse an old tag
git push && git push --tags
```

Avoid `git push --force` once other people (friends, other machines) may have pulled from this
repo — it rewrites history out from under anyone who already has an older clone. Prefer a
forward revert commit + new tag, same pattern as above.

## Tips

- Keep each skill description under 1024 characters (hard limit, blocks install).
- Use a `dev` branch for risky experiments; merge to `main` once promoted. Never push
  half-finished work straight to `main`, friends' installs and your own Cowork can pick up
  `main` at any time.
